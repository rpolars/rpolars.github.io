

# Check whether the data type is an array type

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Check whether the data type is an array type

## Usage

<pre><code class='language-R'>DataType_is_array()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$Array(width = 2)$is_array()
```

    #> [1] TRUE

``` r
pl$Float32$is_array()
```

    #> [1] FALSE
