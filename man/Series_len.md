

# Length of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

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
