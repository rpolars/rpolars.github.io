
# Reduce Boolean Series with ANY

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/series__series.R#L512)

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
