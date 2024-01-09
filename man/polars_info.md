
# Report information of the package

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/info.R#L11)

## Description

This function reports the following information:

<ul>
<li>

Package versions (the R package version and the dependent Rust Polars
version)

</li>
<li>

Number of threads used by Polars

</li>
<li>

Rust feature flags (See <code>vignette(“install”, “polars”)</code> for
details)

</li>
</ul>

## Usage

<pre><code class='language-R'>polars_info()
</code></pre>

## Value

A list with information of the package

## Examples

``` r
library(polars)

polars_info()
```

    #> r-polars package version : 0.12.2
    #> rust-polars crate version: 0.36.2
    #> 
    #> Thread pool size: 4 
    #> 
    #> Features:                         
    #> default              TRUE
    #> full_features        TRUE
    #> simd                 TRUE
    #> sql                  TRUE
    #> rpolars_debug_print FALSE
