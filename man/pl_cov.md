

# Covariance

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/functions__lazy.R#L696)

## Description

Calculates the covariance between two columns / expressions.

## Usage

<pre><code class='language-R'>pl_cov(a, b, ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_cov_:_a">a</code>
</td>
<td>
One column name or Expr or anything convertible Into<Expr> via
<code>pl$col()</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_cov_:_b">b</code>
</td>
<td>
Another column name or Expr or anything convertible Into<Expr> via
<code>pl$col()</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_cov_:_ddof">ddof</code>
</td>
<td>
integer Delta Degrees of Freedom: the divisor used in the calculation is
N - ddof, where N represents the number of elements. By default ddof is
1.
</td>
</tr>
</table>

## Value

Expr for the computed covariance

## Examples

``` r
library(polars)

lf = pl$LazyFrame(data.frame(a = c(1, 8, 3), b = c(4, 5, 2)))
lf$select(pl$cov("a", "b"))$collect()
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 3.0 │
    #> └─────┘

``` r
pl$cov(c(1, 8, 3), c(4, 5, 2))$to_r()
```

    #> [1] 3
