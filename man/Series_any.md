

# Reduce boolean Series with ANY

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L716)

## Description

Reduce boolean Series with ANY

## Usage

<pre><code class='language-R'>Series_any()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

as_polars_series(c(TRUE, FALSE, NA))$any()
```

    #> [1] TRUE
