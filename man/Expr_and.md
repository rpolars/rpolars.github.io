

# Apply logical AND on two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L931)

## Description

Combine two boolean expressions with AND.

## Usage

<pre><code class='language-R'>Expr_and(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="other">other</code>
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

pl$lit(TRUE) & TRUE
```

    #> polars Expr: [(true) & (true)]

``` r
pl$lit(TRUE)$and(pl$lit(TRUE))
```

    #> polars Expr: [(true) & (true)]
