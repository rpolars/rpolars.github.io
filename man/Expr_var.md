
# Get variance

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__expr.R#L1722)

## Description

Get variance

## Usage

<pre><code class='language-R'>Expr_var(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_var_:_ddof">ddof</code>
</td>
<td>
Degrees of freedom, must be an integer between 0 and 255
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
