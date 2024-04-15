

# Length of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

## Description

Length of a Series

## Usage

<pre><code class='language-R'>Series_len()
</code></pre>

## Value

A numeric value

## Examples

``` r
library(polars)

as_polars_series(1:10)$len()
```

    #> [1] 10
