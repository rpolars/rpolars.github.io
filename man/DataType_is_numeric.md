

# Check whether the data type is a numeric type

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Check whether the data type is a numeric type

## Usage

<pre><code class='language-R'>DataType_is_numeric()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$Float32$is_numeric()
```

    #> [1] TRUE

``` r
pl$Int32$is_numeric()
```

    #> [1] TRUE

``` r
pl$String$is_numeric()
```

    #> [1] FALSE
