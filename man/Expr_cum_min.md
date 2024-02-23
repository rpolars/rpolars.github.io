

# Cumulative minimum

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__expr.R#L1333)

## Description

Get an array with the cumulative min computed at every element.

## Usage

<pre><code class='language-R'>Expr_cum_min(reverse = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cum_min_:_reverse">reverse</code>
</td>
<td>
If <code>TRUE</code>, start from the last value.
</td>
</tr>
</table>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
summing to prevent overflow issues.

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(1:4, 2L))$with_columns(
  pl$col("a")$cum_min()$alias("cum_min"),
  pl$col("a")$cum_min(reverse = TRUE)$alias("cum_min_reversed")
)
```

    #> shape: (5, 3)
    #> ┌─────┬─────────┬──────────────────┐
    #> │ a   ┆ cum_min ┆ cum_min_reversed │
    #> │ --- ┆ ---     ┆ ---              │
    #> │ i32 ┆ i32     ┆ i32              │
    #> ╞═════╪═════════╪══════════════════╡
    #> │ 1   ┆ 1       ┆ 1                │
    #> │ 2   ┆ 1       ┆ 2                │
    #> │ 3   ┆ 1       ┆ 2                │
    #> │ 4   ┆ 1       ┆ 2                │
    #> │ 2   ┆ 1       ┆ 2                │
    #> └─────┴─────────┴──────────────────┘
