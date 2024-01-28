

# idx to min value

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L20)

## Description

idx to min value

## Usage

<pre><code class='language-R'>Series_arg_min()
</code></pre>

## Value

bool

## Examples

``` r
library(polars)

pl$Series(c(5, 1))$arg_min()
```

    #> [1] 1
