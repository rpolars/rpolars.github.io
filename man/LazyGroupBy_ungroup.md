

# LazyGroupBy_ungroup

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/lazyframe__group_by.R#L121)

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
