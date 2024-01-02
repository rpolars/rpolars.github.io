
# S3 method to print an Expr

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__expr.R#L43)

## Description

S3 method to print an Expr

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsExpr'
print(x, ...)

Expr_print()
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="print.RPolarsExpr_:_x">x</code>
</td>
<td>
Expr
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="print.RPolarsExpr_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
</table>

## Value

No value returned, it prints in the console.

## Examples

``` r
library(polars)

print(pl$col("some_column")$sum())
```

    #> polars Expr: col("some_column").sum()
