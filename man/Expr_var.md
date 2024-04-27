

# Get variance

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L1678)

## Description

Get variance

## Usage

<pre><code class='language-R'>Expr_var(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ddof">ddof</code>
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

pl$select(pl$lit(1:5)$var())
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │     │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 2.5 │
    #> └─────┘
