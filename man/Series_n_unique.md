
# Count unique values in Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/series__series.R#L995)

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
