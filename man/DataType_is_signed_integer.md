

# Check whether the data type is a signed integer type

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Check whether the data type is a signed integer type

## Usage

<pre><code class='language-R'>DataType_is_signed_integer()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$Int32$is_signed_integer()
```

    #> [1] TRUE

``` r
pl$UInt32$is_signed_integer()
```

    #> [1] FALSE
