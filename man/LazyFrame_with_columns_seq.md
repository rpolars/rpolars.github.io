

# Select and modify columns of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L336)

## Description

Add columns or modify existing ones with expressions. This is the
equivalent of <code>dplyr::mutate()</code> as it keeps unmentioned
columns (unlike <code style="white-space: pre;">$select()</code>).

This will run all expression sequentially instead of in parallel. Use
this when the work per expression is cheap. Otherwise,
<code style="white-space: pre;">$with_columns()</code> should be
preferred.

## Usage

<pre><code class='language-R'>LazyFrame_with_columns_seq(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_with_columns_seq_:_...">…</code>
</td>
<td>
Any expressions or string column name, or same wrapped in a list. If
first and only element is a list, it is unwrapped as a list of args.
</td>
</tr>
</table>

## Value

A LazyFrame

## Examples

``` r
library(polars)

pl$LazyFrame(iris)$with_columns_seq(
  pl$col("Sepal.Length")$abs()$alias("abs_SL"),
  (pl$col("Sepal.Length") + 2)$alias("add_2_SL")
)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #>  WITH_COLUMNS:
    #>  [col("Sepal.Length").abs().alias("abs_SL"), [(col("Sepal.Length")) + (2.0)].alias("add_2_SL")]
    #>   DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"

``` r
# same query
l_expr = list(
  pl$col("Sepal.Length")$abs()$alias("abs_SL"),
  (pl$col("Sepal.Length") + 2)$alias("add_2_SL")
)
pl$LazyFrame(iris)$with_columns_seq(l_expr)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #>  WITH_COLUMNS:
    #>  [col("Sepal.Length").abs().alias("abs_SL"), [(col("Sepal.Length")) + (2.0)].alias("add_2_SL")]
    #>   DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"

``` r
pl$LazyFrame(iris)$with_columns_seq(
  pl$col("Sepal.Length")$abs(), # not named expr will keep name "Sepal.Length"
  SW_add_2 = (pl$col("Sepal.Width") + 2)
)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #>  WITH_COLUMNS:
    #>  [col("Sepal.Length").abs(), [(col("Sepal.Width")) + (2.0)].alias("SW_add_2")]
    #>   DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"
