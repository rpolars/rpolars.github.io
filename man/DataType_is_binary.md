

# Check whether the data type is a binary type

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

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
