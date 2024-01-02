
# Convert a string to titlecase

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__string.R#L275)

## Description

Transform to titlecase variant.

## Usage

<pre><code class='language-R'>ExprStr_to_titlecase()
</code></pre>

## Details

This method is only available with the feature flag "simd" which can be
set via envvar "RPOLARS_FULL_FEATURES" and it requires Rust nightly
toolchain to compile. See <code>pl$polars_info()</code> for more
details.

## Value

Expr of Utf8 titlecase chars

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
