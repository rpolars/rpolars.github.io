

# idx to max value

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

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
