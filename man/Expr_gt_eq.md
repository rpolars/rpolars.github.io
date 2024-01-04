
# Check greater or equal inequality

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/expr__expr.R#L418)

## Description

The RHS can either be an Expr or an object that can be converted to a
literal (e.g an integer).

## Usage

<pre><code class='language-R'>Expr_gt_eq(other)

# S3 method for class 'RPolarsExpr'
e1 &gt;= e2
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gt_eq_:_other">other</code>
</td>
<td>
Literal or object that can be converted to a literal
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gt_eq_:_e1">e1</code>
</td>
<td>
Expr only
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gt_eq_:_e2">e2</code>
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

pl$lit(2) >= 2
```

    #> polars Expr: [(2.0) >= (2.0)]

``` r
pl$lit(2) >= pl$lit(2)
```

    #> polars Expr: [(2.0) >= (2.0)]

``` r
pl$lit(2)$gt_eq(pl$lit(2))
```

    #> polars Expr: [(2.0) >= (2.0)]
