

# Apply logical AND on two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__expr.R#L932)

## Description

Combine two boolean expressions with AND.

## Usage

<pre><code class='language-R'>Expr_and(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_and_:_other">other</code>
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

pl$lit(TRUE) & TRUE
```

    #> polars Expr: [(true) & (true)]

``` r
pl$lit(TRUE)$and(pl$lit(TRUE))
```

    #> polars Expr: [(true) & (true)]
