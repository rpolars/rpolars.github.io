

# Reduce Boolean Series with ALL

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/series__series.R#L693)

## Description

Reduce Boolean Series with ALL

## Usage

<pre><code class='language-R'>Series_all()
</code></pre>

## Value

bool

## Examples

``` r
library(polars)

pl$Series(c(TRUE, TRUE, NA))$all()
```

    #> [1] FALSE
