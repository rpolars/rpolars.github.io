
# Negate a boolean expression

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

The RHS can either be an Expr or an object that can be converted to a
literal (e.g an integer).

## Usage

<pre><code class='language-R'>Expr_not

# S3 method for class 'RPolarsExpr'
!x
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_not_:_x">x</code>
</td>
<td>
Expr
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

# two syntaxes same result
pl$lit(TRUE)$not()
```

    #> polars Expr: true.not()

``` r
!pl$lit(TRUE)
```

    #> polars Expr: true.not()
