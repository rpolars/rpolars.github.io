

# Rolling correlation

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/functions__lazy.R#L750)

## Description

Calculates the rolling correlation between two columns

## Usage

<pre><code class='language-R'>pl_rolling_corr(a, b, window_size, min_periods = NULL, ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_rolling_corr_:_a">a</code>
</td>
<td>
One column name or Expr or anything convertible Into<Expr> via
<code>pl$col()</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_rolling_corr_:_b">b</code>
</td>
<td>
Another column name or Expr or anything convertible Into<Expr> via
<code>pl$col()</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_rolling_corr_:_window_size">window_size</code>
</td>
<td>
int The length of the window
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_rolling_corr_:_min_periods">min_periods</code>
</td>
<td>
NULL or int The number of values in the window that should be non-null
before computing a result. If NULL, it will be set equal to window size.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_rolling_corr_:_ddof">ddof</code>
</td>
<td>
integer Delta Degrees of Freedom: the divisor used in the calculation is
N - ddof, where N represents the number of elements. By default ddof is
1.
</td>
</tr>
</table>

## Value

Expr for the computed rolling correlation

## Examples

``` r
library(polars)

lf = pl$LazyFrame(data.frame(a = c(1, 8, 3), b = c(4, 5, 2)))
lf$select(pl$rolling_corr("a", "b", window_size = 2))$collect()
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ a    │
    #> │ ---  │
    #> │ f64  │
    #> ╞══════╡
    #> │ null │
    #> │ 1.0  │
    #> │ 1.0  │
    #> └──────┘
