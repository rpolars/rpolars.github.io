

# Indicate if an expression has multiple outputs

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__meta.R#L156)

## Description

Indicate if an expression has multiple outputs

## Usage

<pre><code class='language-R'>ExprMeta_has_multiple_outputs()
</code></pre>

## Value

Boolean

## Examples

``` r
library(polars)

e = (pl$col("alice") + pl$col("eve"))$alias("bob")
e$meta$has_multiple_outputs()
```

    #> [1] FALSE

``` r
# pl$all() select multiple cols to modify them, so it has multiple outputs
pl$all()$meta$has_multiple_outputs()
```

    #> [1] TRUE
