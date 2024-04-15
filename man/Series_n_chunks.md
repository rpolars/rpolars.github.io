

# Get the number of chunks that this Series contains.

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

## Description

Get the number of chunks that this Series contains.

## Usage

<pre><code class='language-R'>Series_n_chunks()
</code></pre>

## Value

A numeric value

## Examples

``` r
library(polars)

s = as_polars_series(1:3)
s$n_chunks()
```

    #> [1] 1

``` r
# Concatenate Series with rechunk = TRUE
s2 = as_polars_series(4:6)
pl$concat(s, s2, rechunk = TRUE)$n_chunks()
```

    #> [1] 1

``` r
# Concatenate Series with rechunk = FALSE
pl$concat(s, s2, rechunk = FALSE)$n_chunks()
```

    #> [1] 2
