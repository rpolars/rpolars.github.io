

# Cumulative sum

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__expr.R#L1299)

## Description

Get an array with the cumulative sum computed at every element.

## Usage

<pre><code class='language-R'>Expr_cum_sum(reverse = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cum_sum_:_reverse">reverse</code>
</td>
<td>
If <code>TRUE</code>, start with the total sum of elements and substract
each row one by one.
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

pl$DataFrame(a = 1:4)$with_columns(
  pl$col("a")$cum_sum()$alias("cum_sum"),
  pl$col("a")$cum_sum(reverse = TRUE)$alias("cum_sum_reversed")
)
```

    #> shape: (4, 3)
    #> ┌─────┬─────────┬──────────────────┐
    #> │ a   ┆ cum_sum ┆ cum_sum_reversed │
    #> │ --- ┆ ---     ┆ ---              │
    #> │ i32 ┆ i32     ┆ i32              │
    #> ╞═════╪═════════╪══════════════════╡
    #> │ 1   ┆ 1       ┆ 10               │
    #> │ 2   ┆ 3       ┆ 9                │
    #> │ 3   ┆ 6       ┆ 7                │
    #> │ 4   ┆ 10      ┆ 4                │
    #> └─────┴─────────┴──────────────────┘
