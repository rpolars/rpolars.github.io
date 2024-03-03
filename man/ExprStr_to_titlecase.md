

# Convert a string to titlecase

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__string.R#L272)

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
