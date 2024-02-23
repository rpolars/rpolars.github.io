

# Get standard deviation

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__expr.R#L1749)

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
Degrees of freedom, must be an integer between 0 and 255
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
