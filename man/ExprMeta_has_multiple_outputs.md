

# Has multiple outputs

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__meta.R#L136)

## Description

Whether this expression expands into multiple expressions.

## Usage

<pre><code class='language-R'>ExprMeta_has_multiple_outputs()
</code></pre>

## Value

Bool

## Examples

``` r
library(polars)

pl$all()$meta$has_multiple_outputs()
```

    #> [1] TRUE

``` r
pl$col("some_colname")$meta$has_multiple_outputs()
```

    #> [1] FALSE
