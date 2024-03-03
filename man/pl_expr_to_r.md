

# Convert an Expr to R output

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3094)

## Description

This is mostly useful to debug an expression. It evaluates the Expr in
an empty DataFrame and return the first Series to R. This is an alias
for <code style="white-space: pre;">$to_r()</code>.

## Usage

<pre><code class='language-R'>pl_expr_to_r(expr, df = NULL, i = 0)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_expr_to_r_:_expr">expr</code>
</td>
<td>
An Expr to evaluate.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_expr_to_r_:_df">df</code>
</td>
<td>
If <code>NULL</code> (default), it evaluates the Expr in an empty
DataFrame. Otherwise, provide a DataFrame that the Expr should be
evaluated in.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_expr_to_r_:_i">i</code>
</td>
<td>
Numeric column to extract. Default is zero (which gives the first
column).
</td>
</tr>
</table>

## Value

R object

## Examples

``` r
library(polars)

pl$expr_to_r(pl$lit(1:3))
```

    #> [1] 1 2 3
