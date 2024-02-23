

# Estimated size

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/after-wrappers.R#L20)

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
