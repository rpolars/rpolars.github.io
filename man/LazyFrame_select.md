

# Select and modify columns of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L214)

## Description

Similar to <code>dplyr::mutate()</code>. However, it discards
unmentioned columns (like <code>.()</code> in <code>data.table</code>).

## Usage

<pre><code class='language-R'>LazyFrame_select(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_select_:_...">…</code>
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

pl$LazyFrame(iris)$select(
  pl$col("Sepal.Length")$abs()$alias("abs_SL"),
  (pl$col("Sepal.Length") + 2)$alias("add_2_SL")
)
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #>  SELECT [col("Sepal.Length").abs().alias("abs_SL"), [(col("Sepal.Length")) + (2.0)].alias("add_2_SL")] FROM
    #>   DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"
