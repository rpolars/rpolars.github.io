

# Check inequality

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L430)

## Description

The RHS can either be an Expr or an object that can be converted to a
literal (e.g an integer).

## Usage

<pre><code class='language-R'>Expr_neq(other)

# S3 method for class 'RPolarsExpr'
e1 != e2
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_neq_:_other">other</code>
</td>
<td>
Literal or object that can be converted to a literal
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_neq_:_e1">e1</code>
</td>
<td>
Expr only
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_neq_:_e2">e2</code>
</td>
<td>
Expr or anything that can be converted to a literal
</td>
</tr>
</table>

## Value

Expr

## See Also

Expr_neq_missing

## Examples

``` r
library(polars)

pl$lit(1) != 2
```

    #> polars Expr: [(1.0) != (2.0)]

``` r
pl$lit(1) != pl$lit(2)
```

    #> polars Expr: [(1.0) != (2.0)]

``` r
pl$lit(1)$neq(pl$lit(2))
```

    #> polars Expr: [(1.0) != (2.0)]
