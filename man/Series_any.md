

# Reduce Boolean Series with ANY

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/series__series.R#L506)

## Description

Reduce Boolean Series with ANY

## Usage

<pre><code class='language-R'>Series_any()
</code></pre>

## Value

bool

## Examples

``` r
library(polars)

pl$Series(c(TRUE, FALSE, NA))$any()
```

    #> [1] TRUE
