

# Exponentially-weighted moving variance

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2986)

## Description

Exponentially-weighted moving variance

## Usage

<pre><code class='language-R'>Expr_ewm_var(
  com = NULL,
  span = NULL,
  half_life = NULL,
  alpha = NULL,
  adjust = TRUE,
  bias = FALSE,
  min_periods = 1L,
  ignore_nulls = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_ewm_var_:_com">com</code>
</td>
<td>
Specify decay in terms of center of mass, *γ*, with <code class="reqn">
= ; ; </code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_ewm_var_:_span">span</code>
</td>
<td>
Specify decay in terms of span, *θ*, with $= ; ; $
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_ewm_var_:_half_life">half_life</code>
</td>
<td>
Specify decay in terms of half-life,
:math:<code style="white-space: pre;"></code>, with $ = 1 - { } $ $ ; \>
0$
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_ewm_var_:_alpha">alpha</code>
</td>
<td>
Specify smoothing factor alpha directly, 0 \< *α* ≤ 1.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_ewm_var_:_adjust">adjust</code>
</td>
<td>

Divide by decaying adjustment factor in beginning periods to account for
imbalance in relative weightings:

<ul>
<li>

When <code>adjust=TRUE</code> the EW function is calculatedusing weights
$w_i = (1 - )^i $

</li>
<li>

When <code>adjust=FALSE</code> the EW function is calculated recursively
by <code class="reqn"> y_0 = x_0 \\ y_t = (1 - )y\_{t - 1} + x_t </code>

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_ewm_var_:_bias">bias</code>
</td>
<td>
If <code>FALSE</code>, the calculations are corrected for statistical
bias.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_ewm_var_:_min_periods">min_periods</code>
</td>
<td>
Minimum number of observations in window required to have a value
(otherwise result is null).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_ewm_var_:_ignore_nulls">ignore_nulls</code>
</td>
<td>

Ignore missing values when calculating weights:

<ul>
<li>

When <code>TRUE</code> (default), weights are based on relative
positions. For example, the weights of *x*<sub>0</sub> and
*x*<sub>2</sub> used in calculating the final weighted average of
<code>\[</code> *x*<sub>0</sub>, None,
*x*<sub>2</sub><code style="white-space: pre;">\]</code> are 1 − *α* and
1 if <code>adjust=TRUE</code>, and 1 − *α* and *α* if
<code>adjust=FALSE</code>.

</li>
<li>

When <code>FALSE</code>, weights are based on absolute positions. For
example, the weights of :math:<code>x_0</code> and
:math:<code>x_2</code> used in calculating the final weighted average of
<code>\[</code> *x*<sub>0</sub>, None, *x*<sub>2</sub>\<code
style=“white-space: pre;”\>\]</code> are 1 − *α*)<sup>2</sup> and 1 if
<code>adjust=TRUE</code>, and (1−*α*)<sup>2</sup> and *α* if
<code>adjust=FALSE</code>.

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = 1:3)$
  with_columns(ewm_var = pl$col("a")$ewm_var(com = 1))
```

    #> shape: (3, 2)
    #> ┌─────┬──────────┐
    #> │ a   ┆ ewm_var  │
    #> │ --- ┆ ---      │
    #> │ i32 ┆ f64      │
    #> ╞═════╪══════════╡
    #> │ 1   ┆ 0.0      │
    #> │ 2   ┆ 0.5      │
    #> │ 3   ┆ 0.928571 │
    #> └─────┴──────────┘
