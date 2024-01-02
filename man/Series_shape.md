
# Shape of series

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/series__series.R#L237)

## Description

Shape of series

## Usage

<pre><code class='language-R'>Series_shape()
</code></pre>

## Value

dimension vector of Series

## Examples

``` r
library(polars)

identical(pl$Series(1:2)$shape, 2:1)
```

    #> [1] FALSE
