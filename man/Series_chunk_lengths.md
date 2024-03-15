

# Lengths of Series memory chunks

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Lengths of Series memory chunks

## Usage

<pre><code class='language-R'>Series_chunk_lengths()
</code></pre>

## Value

Numeric vector. Output length is the number of chunks, and the sum of
the output is equal to the length of the full Series.

## Examples

``` r
library(polars)

chunked_series = c(pl$Series(1:3), pl$Series(1:10))
chunked_series$chunk_lengths()
```

    #> [1]  3 10
