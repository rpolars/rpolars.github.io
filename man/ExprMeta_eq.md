

# Check if two expressions are equivalent

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__meta.R#L22)

## Description

Indicate if this expression is the same as another expression. See also
the counterpart <code>$meta$neq()</code>.

## Usage

<pre><code class='language-R'>ExprMeta_eq(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprMeta_eq_:_other">other</code>
</td>
<td>
Expr to compare with
</td>
</tr>
</table>

## Value

A boolean: <code>TRUE</code> if equal, <code>FALSE</code> otherwise

## Examples

``` r
library(polars)

# three naive expression literals
e1 = pl$lit(40) + 2
e2 = pl$lit(42)
e3 = pl$lit(40) + 2

# e1 and e3 are identical expressions
e1$meta$eq(e3)
```

    #> [1] TRUE

``` r
# when evaluated, e1 and e2 are equal
e1$eq(e2)$to_r()
```

    #> [1] TRUE

``` r
# however, on the meta-level, e1 and e2 are NOT identical expressions
e1$meta$eq(e2)
```

    #> [1] FALSE
