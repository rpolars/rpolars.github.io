

# Report information of the package

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/polars_info.R#L17)

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
<li>

Code completion mode: either <code>“deactivated”</code>,
<code>“rstudio”</code>, or <code>“native”</code>. See
<code>polars_code_completion_activate()</code>.

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

    #> Polars R package version : 0.16.0.9000
    #> Rust Polars crate version: 0.39.0
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
    #> 
    #> Code completion: deactivated

``` r
polars_info()$versions
```

    #> $r_package
    #> [1] "0.16.0.9000"
    #> 
    #> $rust_crate
    #> [1] "0.39.0"

``` r
polars_info()$features$nightly
```

    #> [1] TRUE
