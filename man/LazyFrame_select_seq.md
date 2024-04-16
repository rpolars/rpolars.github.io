

# Select and modify columns of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L283)

## Description

Similar to <code>dplyr::mutate()</code>. However, it discards
unmentioned columns (like <code>.()</code> in <code>data.table</code>).

This will run all expression sequentially instead of in parallel. Use
this when the work per expression is cheap. Otherwise,
<code style="white-space: pre;">$select()</code> should be preferred.

## Usage

<pre><code class='language-R'>LazyFrame_select_seq(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_select_seq_:_...">…</code>
</td>
<td>
Columns to keep. Those can be expressions (e.g
<code>pl$col(“a”)</code>), column names (e.g <code>“a”</code>), or list
containing expressions or column names (e.g
<code>list(pl$col(“a”))</code>).
</td>
</tr>
</table>

## Value

A LazyFrame

## Examples

``` r
library(polars)

pl$LazyFrame(iris)$select_seq(
  pl$col("Sepal.Length")$abs()$alias("abs_SL"),
  (pl$col("Sepal.Length") + 2)$alias("add_2_SL")
)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #>  SELECT [col("Sepal.Length").abs().alias("abs_SL"), [(col("Sepal.Length")) + (2.0)].alias("add_2_SL")] FROM
    #>   DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"
