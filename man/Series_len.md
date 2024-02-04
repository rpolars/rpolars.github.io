

# Series_len

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

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
