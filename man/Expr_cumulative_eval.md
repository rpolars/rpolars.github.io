

# Cumulative evaluation of expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3172)

## Description

Run an expression over a sliding window that increases by <code>1</code>
slot every iteration.

## Usage

<pre><code class='language-R'>Expr_cumulative_eval(expr, min_periods = 1L, parallel = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cumulative_eval_:_expr">expr</code>
</td>
<td>
Expression to evaluate.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cumulative_eval_:_min_periods">min_periods</code>
</td>
<td>
Number of valid (non-null) values there should be in the window before
the expression is evaluated.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cumulative_eval_:_parallel">parallel</code>
</td>
<td>
Run in parallel. Don’t do this in a groupby or another operation that
already has much parallelization.
</td>
</tr>
</table>

## Details

This can be really slow as it can have <code>O(n^2)</code> complexity.
Don’t use this for operations that visit all elements.

## Value

Expr

## Examples

``` r
library(polars)

pl$lit(1:5)$cumulative_eval(
  pl$element()$first() - pl$element()$last()^2
)$to_r()
```

    #> [1]   0  -3  -8 -15 -24
