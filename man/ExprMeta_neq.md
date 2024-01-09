
# Meta Not Equal

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__meta.R#L54)

## Description

Are two expressions on a meta level NOT equal

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

bool: TRUE if NOT equal

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
# e_test is an expression testing whether e1 and e2 evaluates to the same value.
e_test = e1 == e2 # or e_test = e1$eq(e2)

# direct evaluate e_test, possible because only made up of literals
e_test$to_r()
```

    #> [1] TRUE

``` r
# e1 and e2 are on the meta-level NOT identical expressions
e1$meta$neq(e2)
```

    #> [1] TRUE
