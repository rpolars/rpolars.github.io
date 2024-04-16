

# Check whether the data type is a primitive type

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Check whether the data type is a primitive type

## Usage

<pre><code class='language-R'>DataType_is_primitive()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$Float32$is_primitive()
```

    #> [1] TRUE

``` r
pl$List()$is_primitive()
```

    #> [1] FALSE
