

# Correlation

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L817)

## Description

Calculates the correlation between two columns

## Usage

<pre><code class='language-R'>pl_corr(a, b, method = "pearson", ddof = 1, propagate_nans = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_corr_:_a">a</code>
</td>
<td>
One column name or Expr or anything convertible Into<Expr> via
<code>pl$col()</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_corr_:_b">b</code>
</td>
<td>
Another column name or Expr or anything convertible Into<Expr> via
<code>pl$col()</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_corr_:_method">method</code>
</td>
<td>
str One of ‘pearson’ or ‘spearman’
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_corr_:_ddof">ddof</code>
</td>
<td>
integer Delta Degrees of Freedom: the divisor used in the calculation is
N - ddof, where N represents the number of elements. By default ddof is
1.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_corr_:_propagate_nans">propagate_nans</code>
</td>
<td>
bool Used only when calculating the spearman rank correlation. If
<code>True</code> any <code>NaN</code> encountered will lead to
<code>NaN</code> in the output. Defaults to <code>False</code> where
<code>NaN</code> are regarded as larger than any finite number and thus
lead to the highest rank.
</td>
</tr>
</table>

## Value

Expr for the computed correlation

## Examples

``` r
library(polars)

lf = pl$LazyFrame(data.frame(a = c(1, 8, 3), b = c(4, 5, 2)))
lf$select(pl$corr("a", "b", method = "spearman"))$collect()
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 0.5 │
    #> └─────┘
