

# Count unique values in Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/series__series.R#L1071)

## Description

Return count of unique values in Series

## Usage

<pre><code class='language-R'>Series_n_unique()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$Series(1:4)$n_unique()
```

    #> [1] 4
