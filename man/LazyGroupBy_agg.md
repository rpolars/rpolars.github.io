

# LazyGroupBy_agg

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__group_by.R#L73)

## Description

aggregate a polar_lazy_group_by

## Usage

<pre><code class='language-R'>LazyGroupBy_agg(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyGroupBy_agg_:_...">…</code>
</td>
<td>
exprs to aggregate over. … args can also be passed wrapped in a list
<code style="white-space: pre;">$agg(list(e1,e2,e3))</code>
</td>
</tr>
</table>

## Value

A new <code>LazyFrame</code> object.

## Examples

``` r
library(polars)

lgb = pl$DataFrame(
  foo = c("one", "two", "two", "one", "two"),
  bar = c(5, 3, 2, 4, 1)
)$
  lazy()$
  group_by("foo")


print(lgb)
```

    #> polars LazyGroupBy: 
    #> LazyGroupBy (internals are opaque)

``` r
lgb$
  agg(
  pl$col("bar")$sum()$name$suffix("_sum"),
  pl$col("bar")$mean()$alias("bar_tail_sum")
)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> AGGREGATE
    #>  [col("bar").sum().alias("bar_sum"), col("bar").mean().alias("bar_tail_sum")] BY [col("foo")] FROM
    #>   DF ["foo", "bar"]; PROJECT */2 COLUMNS; SELECTION: "None"
