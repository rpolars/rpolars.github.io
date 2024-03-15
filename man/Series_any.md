

# Reduce boolean Series with ANY

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L648)

## Description

Reduce boolean Series with ANY

## Usage

<pre><code class='language-R'>Series_any()
</code></pre>

## Value

A boolean scalar

## Examples

``` r
library(polars)

pl$Series(c(TRUE, FALSE, NA))$any()
```

    #> [1] TRUE
