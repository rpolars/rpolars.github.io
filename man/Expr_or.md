

# Apply logical OR on two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__expr.R#L953)

## Description

Combine two boolean expressions with OR.

## Usage

<pre><code class='language-R'>Expr_or(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_or_:_other">other</code>
</td>
<td>
numeric or string value; accepts expression input.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$lit(TRUE) | FALSE
```

    #> polars Expr: [(true) | (false)]

``` r
pl$lit(TRUE)$or(pl$lit(TRUE))
```

    #> polars Expr: [(true) | (true)]
