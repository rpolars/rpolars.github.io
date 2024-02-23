

# idx to max value

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/after-wrappers.R#L20)

## Description

idx to max value

## Usage

<pre><code class='language-R'>Series_arg_max()
</code></pre>

## Value

bool

## Examples

``` r
library(polars)

pl$Series(c(5, 1))$arg_max()
```

    #> [1] 0
