

# Check whether the data type is a temporal type

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Check whether the data type is a temporal type

## Usage

<pre><code class='language-R'>DataType_is_struct()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$Struct()$is_struct()
```

    #> [1] TRUE

``` r
pl$Float32$is_struct()
```

    #> [1] FALSE
