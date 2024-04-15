

# Estimated size

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

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
