

# Estimated size

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L20)

## Description

Return an estimation of the total (heap) allocated size of the
DataFrame.

## Usage

<pre><code class='language-R'>DataFrame_estimated_size()
</code></pre>

## Format

function

## Value

Estimated size in bytes

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$estimated_size()
```

    #> [1] 2816
