

# Index of min value

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Note that this is 0-indexed.

## Usage

<pre><code class='language-R'>Series_arg_min()
</code></pre>

## Value

A numeric value

## Examples

``` r
library(polars)

pl$Series(c(5, 1))$arg_min()
```

    #> [1] 1
