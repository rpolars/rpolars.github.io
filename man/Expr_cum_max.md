

# Cumulative maximum

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1281)

## Description

Get an array with the cumulative max computed at every element.

## Usage

<pre><code class='language-R'>Expr_cum_max(reverse = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cum_max_:_reverse">reverse</code>
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
  pl$col("a")$cum_max()$alias("cummux"),
  pl$col("a")$cum_max(reverse = TRUE)$alias("cum_max_reversed")
)
```

    #> shape: (5, 3)
    #> ┌─────┬────────┬──────────────────┐
    #> │ a   ┆ cummux ┆ cum_max_reversed │
    #> │ --- ┆ ---    ┆ ---              │
    #> │ i32 ┆ i32    ┆ i32              │
    #> ╞═════╪════════╪══════════════════╡
    #> │ 1   ┆ 1      ┆ 4                │
    #> │ 2   ┆ 2      ┆ 4                │
    #> │ 3   ┆ 3      ┆ 4                │
    #> │ 4   ┆ 4      ┆ 4                │
    #> │ 2   ┆ 4      ┆ 2                │
    #> └─────┴────────┴──────────────────┘
