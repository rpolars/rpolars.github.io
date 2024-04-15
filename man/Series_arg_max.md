

# Index of max value

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Note that this is 0-indexed.

## Usage

<pre><code class='language-R'>Series_arg_max()
</code></pre>

## Value

A numeric value

## Examples

``` r
library(polars)

as_polars_series(c(5, 1))$arg_max()
```

    #> [1] 0
