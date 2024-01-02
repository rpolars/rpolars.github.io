
# Reduce Boolean Series with ALL

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/series__series.R#L525)

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
