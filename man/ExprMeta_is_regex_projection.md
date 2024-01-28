

# Is regex projection.

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__meta.R#L150)

## Description

Whether this expression expands to columns that match a regex pattern.

## Usage

<pre><code class='language-R'>ExprMeta_is_regex_projection()
</code></pre>

## Value

Bool

## Examples

``` r
library(polars)

pl$col("^Sepal.*$")$meta$is_regex_projection()
```

    #> [1] TRUE

``` r
pl$col("Sepal.Length")$meta$is_regex_projection()
```

    #> [1] FALSE
