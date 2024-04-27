

# Check whether the data type is a float type

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

## Description

Check whether the data type is a float type

## Usage

<pre><code class='language-R'>DataType_is_float()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$Float32$is_float()
```

    #> [1] TRUE

``` r
pl$Int32$is_float()
```

    #> [1] FALSE
