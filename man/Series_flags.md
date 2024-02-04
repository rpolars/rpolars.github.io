

# Get data type of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L713)

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
