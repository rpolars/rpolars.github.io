

# Print Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/series__series.R#L359)

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

as_polars_series(1:3)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]
