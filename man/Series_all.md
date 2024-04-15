

# Reduce Boolean Series with ALL

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/series__series.R#L725)

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
