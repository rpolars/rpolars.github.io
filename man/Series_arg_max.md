
# idx to max value

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/#L)

## Description

idx to max value

## Usage

<pre><code class='language-R'>Series_arg_max
</code></pre>

## Value

bool

## Examples

``` r
library(polars)

pl$Series(c(5, 1))$arg_max()
```

    #> [1] 0
