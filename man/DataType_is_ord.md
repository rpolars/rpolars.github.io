

# Check whether the data type is an ordinal type

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Check whether the data type is an ordinal type

## Usage

<pre><code class='language-R'>DataType_is_ord()
</code></pre>

## Value

A logical value

## Examples

``` r
library(polars)

pl$String$is_ord()
```

    #> [1] TRUE

``` r
pl$Categorical()$is_ord()
```

    #> [1] FALSE
