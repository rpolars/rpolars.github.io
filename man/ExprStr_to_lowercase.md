

# Convert a string to lowercase

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L258)

## Description

Transform to lowercase variant.

## Usage

<pre><code class='language-R'>ExprStr_to_lowercase()
</code></pre>

## Value

Expr of String lowercase chars

## Examples

``` r
library(polars)

pl$lit(c("A", "b", "c", "1", NA))$str$to_lowercase()$to_series()
```

    #> polars Series: shape: (5,)
    #> Series: '' [str]
    #> [
    #>  "a"
    #>  "b"
    #>  "c"
    #>  "1"
    #>  null
    #> ]
