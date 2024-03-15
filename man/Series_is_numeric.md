

# Check if the Series is numeric

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L962)

## Description

This checks whether the Series DataType is in
<code>pl$numeric_dtypes</code>.

## Usage

<pre><code class='language-R'>Series_is_numeric()
</code></pre>

## Value

A boolean scalar

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
