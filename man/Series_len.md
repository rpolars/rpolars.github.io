
# Series_len

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/#L)

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
