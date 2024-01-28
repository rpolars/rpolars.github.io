

# Disable the global string cache

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/polars_options.R#L357)

## Description

Some functions (e.g joins) can be applied on Categorical series only
allowed if using the global string cache is enabled. This function
disables the string_cache. In general, you should use
<code>pl$with_string_cache()</code> instead.

## Usage

<pre><code class='language-R'>pl_disable_string_cache()
</code></pre>

## Value

This doesn’t return any value.

## See Also

<code>pl$using_string_cache</code> <code>pl$enable_string_cache</code>
<code>pl$with_string_cache</code>

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
