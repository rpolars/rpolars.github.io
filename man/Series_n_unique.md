

# Count unique values in Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L989)

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
