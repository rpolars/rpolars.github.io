

# Shape of series

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L236)

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
