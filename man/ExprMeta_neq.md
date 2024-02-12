

# Check if two expressions are different

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/expr__meta.R#L48)

## Description

Indicate if this expression is different from another expression. See
also the counterpart <code>$meta$eq()</code>.

## Usage

<pre><code class='language-R'>ExprMeta_neq(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprMeta_neq_:_other">other</code>
</td>
<td>
Expr to compare with
</td>
</tr>
</table>

## Value

A boolean: <code>TRUE</code> if different, <code>FALSE</code> otherwise

## Examples

``` r
library(polars)

# three naive expression literals
e1 = pl$lit(40) + 2
e2 = pl$lit(42)
e3 = pl$lit(40) + 2

# e1 and e3 are identical expressions
e1$meta$neq(e3)
```

    #> [1] FALSE

``` r
# when evaluated, e1 and e2 are equal
e1$neq(e2)$to_r()
```

    #> [1] FALSE

``` r
# however, on the meta-level, e1 and e2 are different
e1$meta$neq(e2)
```

    #> [1] TRUE
