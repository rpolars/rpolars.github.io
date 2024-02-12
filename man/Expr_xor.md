

# Apply logical XOR on two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/expr__expr.R#L964)

## Description

Combine two boolean expressions with XOR.

## Usage

<pre><code class='language-R'>Expr_xor(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_xor_:_other">other</code>
</td>
<td>
Literal or object that can be converted to a literal
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$lit(TRUE)$xor(pl$lit(FALSE))
```

    #> polars Expr: [(true) ^ (false)]
