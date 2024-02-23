

# Convert a string to titlecase

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__string.R#L273)

## Description

Transform to titlecase variant.

## Usage

<pre><code class='language-R'>ExprStr_to_titlecase()
</code></pre>

## Details

This method is only available with the "nightly" feature. See
<code>polars_info()</code> for more details.

## Value

Expr of String titlecase chars

## Examples

``` r
library(polars)


pl$lit(c("hello there", "HI, THERE", NA))$str$to_titlecase()$to_series()
```

    #> polars Series: shape: (3,)
    #> Series: '' [str]
    #> [
    #>  "Hello There"
    #>  "Hi, There"
    #>  null
    #> ]
