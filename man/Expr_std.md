

# Get standard deviation

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1752)

## Description

Get standard deviation

## Usage

<pre><code class='language-R'>Expr_std(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_std_:_ddof">ddof</code>
</td>
<td>
An integer representing "Delta Degrees of Freedom": the divisor used in
the calculation is <code>N - ddof</code>, where <code>N</code>
represents the number of elements. By default ddof is <code>1</code>.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$select(pl$lit(1:5)$std())
```

    #> shape: (1, 1)
    #> ┌──────────┐
    #> │          │
    #> │ ---      │
    #> │ f64      │
    #> ╞══════════╡
    #> │ 1.581139 │
    #> └──────────┘
