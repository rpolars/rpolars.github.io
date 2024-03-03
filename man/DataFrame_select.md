

# Select and modify columns of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/dataframe__frame.R#L699)

## Description

Similar to <code>dplyr::mutate()</code>. However, it discards
unmentioned columns (like <code>.()</code> in <code>data.table</code>).

## Usage

<pre><code class='language-R'>DataFrame_select(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_select_:_...">…</code>
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

DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(iris)$select(
  pl$col("Sepal.Length")$abs()$alias("abs_SL"),
  (pl$col("Sepal.Length") + 2)$alias("add_2_SL")
)
```

    #> shape: (150, 2)
    #> ┌────────┬──────────┐
    #> │ abs_SL ┆ add_2_SL │
    #> │ ---    ┆ ---      │
    #> │ f64    ┆ f64      │
    #> ╞════════╪══════════╡
    #> │ 5.1    ┆ 7.1      │
    #> │ 4.9    ┆ 6.9      │
    #> │ 4.7    ┆ 6.7      │
    #> │ 4.6    ┆ 6.6      │
    #> │ 5.0    ┆ 7.0      │
    #> │ …      ┆ …        │
    #> │ 6.7    ┆ 8.7      │
    #> │ 6.3    ┆ 8.3      │
    #> │ 6.5    ┆ 8.5      │
    #> │ 6.2    ┆ 8.2      │
    #> │ 5.9    ┆ 7.9      │
    #> └────────┴──────────┘
