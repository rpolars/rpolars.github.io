

# Accumulate over multiple columns horizontally with an R function

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/functions__lazy.R#L864)

## Description

This allows one to do rowwise operations, starting with an initial value
(<code>acc</code>). See <code>pl$reduce()</code> to do rowwise
operations without this initial value.

## Usage

<pre><code class='language-R'>pl_fold(acc, lambda, exprs)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_fold_:_acc">acc</code>
</td>
<td>
an Expr or Into<Expr> of the initial accumulator.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_fold_:_lambda">lambda</code>
</td>
<td>
R function which takes two polars Series as input and return one.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_fold_:_exprs">exprs</code>
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
  pl$fold(
    acc = pl$lit(0),
    lambda = \(acc, x) acc + x,
    exprs = pl$col("*")
  )$alias("mpg_drat_sum_folded")
)
```

    #> shape: (32, 12)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬──────┬──────┬─────────────────────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ am  ┆ gear ┆ carb ┆ mpg_drat_sum_folded │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ ---  ┆ ---  ┆ ---                 │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64  ┆ f64  ┆ f64                 │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪══════╪══════╪═════════════════════╡
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 4.0  ┆ 328.98              │
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 4.0  ┆ 329.795             │
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 4.0  ┆ 1.0  ┆ 259.58              │
    #> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 3.0  ┆ 1.0  ┆ 426.135             │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …    ┆ …    ┆ …                   │
    #> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 4.0  ┆ 670.69              │
    #> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 6.0  ┆ 379.59              │
    #> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 8.0  ┆ 694.71              │
    #> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 2.0  ┆ 288.89              │
    #> └──────┴─────┴───────┴───────┴───┴─────┴──────┴──────┴─────────────────────┘
