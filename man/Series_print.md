

# Print Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L76)

## Description

Print Series

## Usage

<pre><code class='language-R'>Series_print()
</code></pre>

## Value

self

## Examples

``` r
library(polars)

pl$Series(1:3)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]
