

# LazyGroupBy_ungroup

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/lazyframe__group_by.R#L121)

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

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
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

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
