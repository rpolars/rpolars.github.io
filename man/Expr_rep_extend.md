
# Extend a Series by repeating values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3168)

## Description

Extend a Series by repeating values

## Usage

<pre><code class='language-R'>Expr_rep_extend(expr, n, rechunk = TRUE, upcast = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rep_extend_:_expr">expr</code>
</td>
<td>
Expr or something coercible to an Expr.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rep_extend_:_n">n</code>
</td>
<td>
The number of times to repeat, must be non-negative and finite.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rep_extend_:_rechunk">rechunk</code>
</td>
<td>
If <code>TRUE</code> (default), memory layout will be rewritten.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rep_extend_:_upcast">upcast</code>
</td>
<td>
If <code>TRUE</code> (default), non identical types will be cast to
common supertype if there is any. If <code>FALSE</code> or no common
super type, having different types will throw an error.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$select(pl$lit(c(1, 2, 3))$rep_extend(1:3, n = 5))
```

    #> shape: (18, 1)
    #> ┌─────┐
    #> │     │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> │ 2.0 │
    #> │ 3.0 │
    #> │ 1.0 │
    #> │ …   │
    #> │ 3.0 │
    #> │ 1.0 │
    #> │ 2.0 │
    #> │ 3.0 │
    #> └─────┘
