

# Lengths of Series memory chunks

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/after-wrappers.R#L20)

## Description

Get the Lengths of Series memory chunks as vector.

## Usage

<pre><code class='language-R'>Series_chunk_lengths()
</code></pre>

## Value

numeric vector. Length is number of chunks. Sum of lengths is equal to
size of Series.

## Examples

``` r
library(polars)

chunked_series = c(pl$Series(1:3), pl$Series(1:10))
chunked_series$chunk_lengths()
```

    #> [1]  3 10
