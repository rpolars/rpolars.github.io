

# is_numeric

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L886)

## Description

return bool whether series is numeric

## Usage

<pre><code class='language-R'>Series_is_numeric()
</code></pre>

## Format

method

## Details

true of series dtype is member of pl$numeric_dtypes

## Value

bool

## Examples

``` r
library(polars)

pl$Series(1:4)$is_numeric()
```

    #> [1] TRUE

``` r
pl$Series(c("a", "b", "c"))$is_numeric()
```

    #> [1] FALSE

``` r
pl$numeric_dtypes
```

    #> $Int8
    #> DataType: Int8
    #> 
    #> $Int16
    #> DataType: Int16
    #> 
    #> $Int32
    #> DataType: Int32
    #> 
    #> $Int64
    #> DataType: Int64
    #> 
    #> $Float32
    #> DataType: Float32
    #> 
    #> $Float64
    #> DataType: Float64
