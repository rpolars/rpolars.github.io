
# Report information of the package

## Description

Report information of the package

## Usage

<pre><code class='language-R'>pl_polars_info()
</code></pre>

## Value

A list with information of the package

## Examples

``` r
library(polars)

pl$polars_info()
```

    #> r-polars package version : 0.12.0.9000
    #> rust-polars crate version: 0.35.4
    #> 
    #> Thread pool size: 4 
    #> 
    #> Features:                         
    #> default              TRUE
    #> full_features        TRUE
    #> simd                 TRUE
    #> sql                  TRUE
    #> rpolars_debug_print FALSE
