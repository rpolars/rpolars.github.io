

# Check strictly greater inequality

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L319)

## Description

The RHS can either be an Expr or an object that can be converted to a
literal (e.g an integer).

## Usage

<pre><code class='language-R'>Expr_gt(other)

# S3 method for class 'RPolarsExpr'
e1 &gt; e2
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gt_:_other">other</code>
</td>
<td>
Literal or object that can be converted to a literal
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gt_:_e1">e1</code>
</td>
<td>
Expr only
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gt_:_e2">e2</code>
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

pl$lit(2) > 1
```

    #> polars Expr: [(2.0) > (1.0)]

``` r
pl$lit(2) > pl$lit(1)
```

    #> polars Expr: [(2.0) > (1.0)]

``` r
pl$lit(2)$gt(pl$lit(1))
```

    #> polars Expr: [(2.0) > (1.0)]
