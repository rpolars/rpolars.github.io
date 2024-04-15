

# Get optimization settings

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/lazyframe__lazy.R#L391)

## Description

Get the current optimization toggles for the lazy query

## Usage

<pre><code class='language-R'>LazyFrame_get_optimization_toggle()
</code></pre>

## Value

List of optimization toggles

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$get_optimization_toggle()
```

    #> $type_coercion
    #> [1] TRUE
    #> 
    #> $predicate_pushdown
    #> [1] TRUE
    #> 
    #> $projection_pushdown
    #> [1] TRUE
    #> 
    #> $simplify_expression
    #> [1] TRUE
    #> 
    #> $slice_pushdown
    #> [1] TRUE
    #> 
    #> $comm_subplan_elim
    #> [1] TRUE
    #> 
    #> $comm_subexpr_elim
    #> [1] TRUE
    #> 
    #> $streaming
    #> [1] FALSE
    #> 
    #> $eager
    #> [1] FALSE
