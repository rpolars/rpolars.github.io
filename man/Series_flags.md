

# Get data type of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L698)

## Description

Get data type of Series

## Usage

<pre><code class='language-R'>Series_flags()
</code></pre>

## Details

property sorted flags are not settable, use set_sorted

## Value

DataType

## Examples

``` r
library(polars)

pl$Series(1:4)$sort()$flags
```

    #> $SORTED_ASC
    #> [1] TRUE
    #> 
    #> $SORTED_DESC
    #> [1] FALSE
