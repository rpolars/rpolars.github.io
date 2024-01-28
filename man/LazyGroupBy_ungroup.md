

# LazyGroupBy_ungroup

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/lazyframe__group_by.R#L94)

## Description

Revert the group by operation.

## Usage

<pre><code class='language-R'>LazyGroupBy_ungroup()
</code></pre>

## Value

A new <code>LazyFrame</code> object.

## Examples

``` r
library(polars)

lf = pl$LazyFrame(mtcars)
lf
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"

``` r
lgb = lf$group_by("cyl")
lgb
```

    #> polars LazyGroupBy: 
    #> LazyGroupBy (internals are opaque)

``` r
lgb$ungroup()
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
