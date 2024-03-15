

# Reduce Boolean Series with ALL

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L657)

## Description

Reduce Boolean Series with ALL

## Usage

<pre><code class='language-R'>Series_all()
</code></pre>

## Value

A boolean scalar

## Examples

``` r
library(polars)

pl$Series(c(TRUE, TRUE, NA))$all()
```

    #> [1] FALSE
