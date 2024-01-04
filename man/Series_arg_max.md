
# idx to max value

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/#L)

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
