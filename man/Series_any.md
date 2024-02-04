

# Reduce Boolean Series with ANY

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L506)

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
