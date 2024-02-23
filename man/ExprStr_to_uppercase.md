

# Convert a string to uppercase

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__string.R#L248)

## Description

Transform to uppercase variant.

## Usage

<pre><code class='language-R'>ExprStr_to_uppercase()
</code></pre>

## Value

Expr of String uppercase chars

## Examples

``` r
library(polars)

pl$lit(c("A", "b", "c", "1", NA))$str$to_uppercase()$to_series()
```

    #> polars Series: shape: (5,)
    #> Series: '' [str]
    #> [
    #>  "A"
    #>  "B"
    #>  "C"
    #>  "1"
    #>  null
    #> ]
