

# Check whether the data type is a null type

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Check whether the data type is a null type

## Usage

<pre><code class='language-R'>DataType_is_null()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$Null$is_null()
```

    #> [1] TRUE

``` r
pl$Float32$is_null()
```

    #> [1] FALSE
