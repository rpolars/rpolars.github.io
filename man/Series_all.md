

# Reduce Boolean Series with ALL

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L518)

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
