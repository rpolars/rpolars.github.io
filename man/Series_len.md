

# Series_len

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L20)

## Description

Length of this Series.

## Usage

<pre><code class='language-R'>Series_len()
</code></pre>

## Value

numeric

## Examples

``` r
library(polars)

pl$Series(1:10)$len()
```

    #> [1] 10
