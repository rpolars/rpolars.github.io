

# Check whether the data type is a signed integer type

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

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
