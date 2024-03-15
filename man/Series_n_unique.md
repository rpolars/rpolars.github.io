

# Count unique values in Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L987)

## Description

Count unique values in Series

## Usage

<pre><code class='language-R'>Series_n_unique()
</code></pre>

## Value

A numeric scalar

## Examples

``` r
library(polars)

pl$Series(c(1, 2, 1, 4, 4, 1, 5))$n_unique()
```

    #> [1] 4
