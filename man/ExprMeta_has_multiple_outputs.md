

# Indicate if an expression has multiple outputs

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__meta.R#L156)

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
