

# Convert a string to lowercase

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__string.R#L11)

## Description

Transform to lowercase variant.

## Usage

<pre><code class='language-R'>SeriesStr_to_lowercase()
</code></pre>

## Value

Expr of String lowercase chars

## Examples

``` r
library(polars)

pl$Series(c("A", "B", "C"))$str$to_lowercase()
```

    #> polars Series: shape: (3,)
    #> Series: '' [str]
    #> [
    #>  "a"
    #>  "b"
    #>  "c"
    #> ]
