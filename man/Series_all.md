

# Reduce Boolean Series with ALL

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/series__series.R#L725)

## Description

Reduce Boolean Series with ALL

## Usage

<pre><code class='language-R'>Series_all()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

as_polars_series(c(TRUE, TRUE, NA))$all()
```

    #> [1] FALSE
