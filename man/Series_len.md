
# Series_len

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

Length of this Series.

## Usage

<pre><code class='language-R'>Series_len
</code></pre>

## Value

numeric

## Examples

``` r
library(polars)

pl$Series(1:10)$len()
```

    #> [1] 10
