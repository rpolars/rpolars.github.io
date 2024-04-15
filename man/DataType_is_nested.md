

# Check whether the data type is a nested type

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Check whether the data type is a nested type

## Usage

<pre><code class='language-R'>DataType_is_nested()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$List()$is_nested()
```

    #> [1] TRUE

``` r
pl$Array(width = 2)$is_nested()
```

    #> [1] TRUE

``` r
pl$Float32$is_nested()
```

    #> [1] FALSE
