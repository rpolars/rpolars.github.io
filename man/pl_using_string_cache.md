

# Check if the global string cache is enabled

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/polars_options.R#L298)

## Description

This function simply checks if the global string cache is active.

## Usage

<pre><code class='language-R'>pl_using_string_cache()
</code></pre>

## Value

A logical value

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
