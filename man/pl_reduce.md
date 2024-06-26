

# Accumulate over multiple columns horizontally with an R function

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L823)

## Description

This allows one to do rowwise operations. See <code>pl$fold()</code> to
do rowwise operations with an initial value.

## Usage

<pre><code class='language-R'>pl_reduce(lambda, exprs)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="lambda">lambda</code>
</td>
<td>
R function which takes two polars Series as input and return one.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="exprs">exprs</code>
</td>
<td>
Expressions to aggregate over. May also be a wildcard expression.
</td>
</tr>
</table>

## Value

An expression that will be applied rowwise

## Examples

``` r
library(polars)

df = pl$DataFrame(mtcars)

# Make the row-wise sum of all columns
df$with_columns(
  pl$reduce(
    lambda = \(acc, x) acc + x,
    exprs = pl$col("*")
  )$alias("mpg_drat_sum_reduced")
)
```

    #> shape: (32, 12)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬──────┬──────┬──────────────────────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ am  ┆ gear ┆ carb ┆ mpg_drat_sum_reduced │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ ---  ┆ ---  ┆ ---                  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64  ┆ f64  ┆ f64                  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪══════╪══════╪══════════════════════╡
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 4.0  ┆ 328.98               │
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 4.0  ┆ 329.795              │
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 4.0  ┆ 1.0  ┆ 259.58               │
    #> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 3.0  ┆ 1.0  ┆ 426.135              │
    #> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 3.0  ┆ 2.0  ┆ 590.31               │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …    ┆ …    ┆ …                    │
    #> │ 30.4 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 2.0  ┆ 273.683              │
    #> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 4.0  ┆ 670.69               │
    #> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 6.0  ┆ 379.59               │
    #> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 8.0  ┆ 694.71               │
    #> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 2.0  ┆ 288.89               │
    #> └──────┴─────┴───────┴───────┴───┴─────┴──────┴──────┴──────────────────────┘
