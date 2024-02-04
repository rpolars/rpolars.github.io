

# Count unique values in Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L1004)

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
