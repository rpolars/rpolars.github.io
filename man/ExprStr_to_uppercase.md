

# Convert a string to uppercase

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__string.R#L257)

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
