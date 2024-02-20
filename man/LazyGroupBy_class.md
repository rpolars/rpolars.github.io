

# Operations on Polars grouped LazyFrame

## Description

This class comes from <code>\<LazyFrame\>$group_by()</code>, etc.

## Active bindings

<h4>
columns
</h4>

<code style="white-space: pre;">$columns</code> returns a character
vector with the column names.

## Examples

``` r
library(polars)

as_polars_lf(mtcars)$group_by("cyl")$agg(
  pl$col("mpg")$sum()
)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> AGGREGATE
    #>  [col("mpg").sum()] BY [col("cyl")] FROM
    #>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
