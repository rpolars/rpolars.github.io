

# Check whether the data type is a boolean type

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

## Description

Check whether the data type is a boolean type

## Usage

<pre><code class='language-R'>DataType_is_bool()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$Boolean$is_bool()
```

    #> [1] TRUE

``` r
pl$Float32$is_bool()
```

    #> [1] FALSE
