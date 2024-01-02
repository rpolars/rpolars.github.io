
# Lengths of Series memory chunks

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/#L)

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
