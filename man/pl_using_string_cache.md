
# Check if the global string cache is enabled

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/options.R#L269)

## Description

This function simply checks if the global string cache is active.

## Usage

<pre><code class='language-R'>pl_using_string_cache()
</code></pre>

## Value

A boolean

## See Also

<code>pl$with_string_cache</code> <code>pl$enable_enable_cache</code>

## Examples

``` r
library(polars)

pl$enable_string_cache()
pl$using_string_cache()
```

    #> [1] TRUE

``` r
pl$disable_string_cache()
pl$using_string_cache()
```

    #> [1] FALSE
