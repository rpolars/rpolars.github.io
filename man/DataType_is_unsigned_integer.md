

# Check whether the data type is an unsigned integer type

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

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
