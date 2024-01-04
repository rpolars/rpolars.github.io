
# Reduce Boolean Series with ALL

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/series__series.R#L524)

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
