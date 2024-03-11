

# Estimated size

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/after-wrappers.R#L20)

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
