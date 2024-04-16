

# Indicate if an expression uses a regex projection

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__meta.R#L167)

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
