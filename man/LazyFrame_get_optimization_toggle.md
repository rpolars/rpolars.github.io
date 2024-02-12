

# Get optimization settings

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/lazyframe__lazy.R#L303)

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
