

# Indicate if an expression uses a regex projection

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__meta.R#L139)

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
