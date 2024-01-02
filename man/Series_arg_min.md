
# idx to min value

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

idx to min value

## Usage

<pre><code class='language-R'>Series_arg_min
</code></pre>

## Value

bool

## Examples

``` r
library(polars)

pl$Series(c(5, 1))$arg_min()
```

    #> [1] 1
