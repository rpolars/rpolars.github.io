

# Indicate if an expression uses a regex projection

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/expr__meta.R#L139)

## Description

Indicate if an expression uses a regex projection

## Usage

<pre><code class='language-R'>ExprMeta_is_regex_projection()
</code></pre>

## Value

Boolean

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
