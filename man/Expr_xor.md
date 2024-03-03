

# Apply logical XOR on two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__expr.R#L1034)

## Description

Combine two boolean expressions with XOR.

## Usage

<pre><code class='language-R'>Expr_xor(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_xor_:_other">other</code>
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

pl$lit(TRUE)$xor(pl$lit(FALSE))
```

    #> polars Expr: [(true) ^ (false)]
