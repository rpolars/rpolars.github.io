
# Add two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L165)

## Description

The RHS can either be an Expr or an object that can be converted to a
literal (e.g an integer).

## Usage

<pre><code class='language-R'>Expr_add(other)

# S3 method for class 'RPolarsExpr'
e1 + e2
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_add_:_other">other</code>
</td>
<td>
Literal or object that can be converted to a literal
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_add_:_e1">e1</code>
</td>
<td>
Expr only
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_add_:_e2">e2</code>
</td>
<td>
Expr or anything that can be converted to a literal
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$lit(5) + 10
```

    #> polars Expr: [(5.0) + (10.0)]

``` r
pl$lit(5) + pl$lit(10)
```

    #> polars Expr: [(5.0) + (10.0)]

``` r
pl$lit(5)$add(pl$lit(10))
```

    #> polars Expr: [(5.0) + (10.0)]

``` r
+pl$lit(5) # unary use resolves to same as pl$lit(5)
```

    #> polars Expr: 5.0
