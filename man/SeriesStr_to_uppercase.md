

# Convert a string to uppercase

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__string.R#L4)

## Description

Transform to uppercase variant.

## Usage

<pre><code class='language-R'>SeriesStr_to_uppercase()
</code></pre>

## Value

Expr of String uppercase chars

## Examples

``` r
library(polars)

pl$Series(c("a", "b", "c"))$str$to_uppercase()
```

    #> polars Series: shape: (3,)
    #> Series: '' [str]
    #> [
    #>  "A"
    #>  "B"
    #>  "C"
    #> ]
