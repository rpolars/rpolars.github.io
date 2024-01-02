
# Accumulate over multiple columns horizontally with an R function

## Description

<code>pl$fold()</code> and <code>pl$reduce()</code> allows one to do
rowwise operations. The only difference between them is that
<code>pl$fold()</code> has an additional argument (<code>acc</code>)
that contains the value that will be initialized when the fold starts.

## Usage

<pre><code class='language-R'>pl_fold(acc, lambda, exprs)

pl_reduce(lambda, exprs)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_fold_reduce_:_acc">acc</code>
</td>
<td>
an Expr or Into<Expr> of the initial accumulator.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_fold_reduce_:_lambda">lambda</code>
</td>
<td>
R function which takes two polars Series as input and return one.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_fold_reduce_:_exprs">exprs</code>
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

# Make the row-wise sum of all columns with fold, reduce and vectorized "+"
df$with_columns(
  pl$reduce(
    lambda = \(acc, x) acc + x,
    exprs = pl$col("mpg", "drat")
  )$alias("mpg_drat_sum_reduced"),
  pl$fold(
    acc = pl$lit(0),
    lambda = \(acc, x) acc + x,
    exprs = pl$col("mpg", "drat")
  )$alias("mpg_drat_sum_folded"),
  (pl$col("mpg") + pl$col("drat"))$alias("mpg_drat_vector_sum")
)
```

    #> shape: (32, 14)
    #> ┌──────┬─────┬───────┬───────┬───┬──────┬───────────────────┬───────────────────┬──────────────────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ carb ┆ mpg_drat_sum_redu ┆ mpg_drat_sum_fold ┆ mpg_drat_vector_ │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ ---  ┆ ced               ┆ ed                ┆ sum              │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64  ┆ ---               ┆ ---               ┆ ---              │
    #> │      ┆     ┆       ┆       ┆   ┆      ┆ f64               ┆ f64               ┆ f64              │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪══════╪═══════════════════╪═══════════════════╪══════════════════╡
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 4.0  ┆ 24.9              ┆ 24.9              ┆ 24.9             │
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 4.0  ┆ 24.9              ┆ 24.9              ┆ 24.9             │
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0  ┆ 26.65             ┆ 26.65             ┆ 26.65            │
    #> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0  ┆ 24.48             ┆ 24.48             ┆ 24.48            │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …    ┆ …                 ┆ …                 ┆ …                │
    #> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 4.0  ┆ 20.02             ┆ 20.02             ┆ 20.02            │
    #> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 6.0  ┆ 23.32             ┆ 23.32             ┆ 23.32            │
    #> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 8.0  ┆ 18.54             ┆ 18.54             ┆ 18.54            │
    #> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 2.0  ┆ 25.51             ┆ 25.51             ┆ 25.51            │
    #> └──────┴─────┴───────┴───────┴───┴──────┴───────────────────┴───────────────────┴──────────────────┘
