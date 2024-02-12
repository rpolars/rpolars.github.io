

# Series_len

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/after-wrappers.R#L20)

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
