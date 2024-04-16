

# Check whether the data type is an unsigned integer type

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Check whether the data type is an unsigned integer type

## Usage

<pre><code class='language-R'>DataType_is_unsigned_integer()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$UInt32$is_unsigned_integer()
```

    #> [1] TRUE

``` r
pl$Int32$is_unsigned_integer()
```

    #> [1] FALSE
