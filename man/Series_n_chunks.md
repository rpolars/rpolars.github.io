

# Get the number of chunks that this Series contains.

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

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
