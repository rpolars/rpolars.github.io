

# Check whether the data type is a binary type

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

## Description

Check whether the data type is a binary type

## Usage

<pre><code class='language-R'>DataType_is_binary()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$Binary$is_binary()
```

    #> [1] TRUE

``` r
pl$Float32$is_binary()
```

    #> [1] FALSE
