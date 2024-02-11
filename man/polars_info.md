

# Report information of the package

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/polars_info.R#L15)

## Description

This function reports the following information:

<ul>
<li>

Package versions (the Polars R package version and the dependent Rust
Polars crate version)

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

    #> Polars R package version : 0.13.1.9000
    #> Rust Polars crate version: 0.37.0
    #> 
    #> Thread pool size: 4 
    #> 
    #> Features:                               
    #> default                    TRUE
    #> full_features              TRUE
    #> disable_limit_max_threads  TRUE
    #> nightly                    TRUE
    #> sql                        TRUE
    #> rpolars_debug_print       FALSE

``` r
polars_info()$rust_polars
```

    #> NULL

``` r
polars_info()$features$nightly
```

    #> [1] TRUE
