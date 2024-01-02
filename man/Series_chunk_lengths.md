
# Lengths of Series memory chunks

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

Get the Lengths of Series memory chunks as vector.

## Usage

<pre><code class='language-R'>Series_chunk_lengths
</code></pre>

## Format

An object of class <code>character</code> of length 1.

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
