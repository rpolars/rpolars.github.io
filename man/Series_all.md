

# Reduce Boolean Series with ALL

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L518)

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
