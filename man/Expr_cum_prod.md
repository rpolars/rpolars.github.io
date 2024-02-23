

# Cumulative product

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__expr.R#L1317)

## Description

Get an array with the cumulative product computed at every element.

## Usage

<pre><code class='language-R'>Expr_cum_prod(reverse = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cum_prod_:_reverse">reverse</code>
</td>
<td>
If <code>TRUE</code>, start with the total product of elements and
divide each row one by one.
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
  pl$col("a")$cum_prod()$alias("cum_prod"),
  pl$col("a")$cum_prod(reverse = TRUE)$alias("cum_prod_reversed")
)
```

    #> shape: (4, 3)
    #> ┌─────┬──────────┬───────────────────┐
    #> │ a   ┆ cum_prod ┆ cum_prod_reversed │
    #> │ --- ┆ ---      ┆ ---               │
    #> │ i32 ┆ i64      ┆ i64               │
    #> ╞═════╪══════════╪═══════════════════╡
    #> │ 1   ┆ 1        ┆ 24                │
    #> │ 2   ┆ 2        ┆ 24                │
    #> │ 3   ┆ 6        ┆ 12                │
    #> │ 4   ┆ 24       ┆ 4                 │
    #> └─────┴──────────┴───────────────────┘
