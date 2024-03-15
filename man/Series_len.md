

# Length of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

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

pl$Series(1:10)$len()
```

    #> [1] 10
