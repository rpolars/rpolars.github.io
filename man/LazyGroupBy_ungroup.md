
# LazyGroupBy_ungroup

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/lazyframe__group_by.R#L95)

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
