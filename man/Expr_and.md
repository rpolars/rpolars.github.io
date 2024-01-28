

# Apply logical AND on two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__expr.R#L932)

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
