

# Aggregate over a RollingGroupBy

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/group_by_rolling.R#L93)

## Description

Aggregate a DataFrame over a rolling window created with
<code style="white-space: pre;">$rolling()</code>.

## Usage

<pre><code class='language-R'>RollingGroupBy_agg(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="RollingGroupBy_agg_:_...">…</code>
</td>
<td>
Exprs to aggregate over. Those can also be passed wrapped in a list, e.g
<code style="white-space: pre;">$agg(list(e1,e2,e3))</code>.
</td>
</tr>
</table>

## Value

An aggregated DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  dt = c("2020-01-01", "2020-01-01", "2020-01-01", "2020-01-02", "2020-01-03", "2020-01-08"),
  a = c(3, 7, 5, 9, 2, 1)
)$with_columns(
  pl$col("dt")$str$strptime(pl$Date, format = NULL)$set_sorted()
)

df$rolling(index_column = "dt", period = "2d")$agg(
  pl$col("a"),
  pl$sum("a")$alias("sum_a"),
  pl$min("a")$alias("min_a"),
  pl$max("a")$alias("max_a")
)
```

    #> shape: (6, 5)
    #> ┌────────────┬───────────────────┬───────┬───────┬───────┐
    #> │ dt         ┆ a                 ┆ sum_a ┆ min_a ┆ max_a │
    #> │ ---        ┆ ---               ┆ ---   ┆ ---   ┆ ---   │
    #> │ date       ┆ list[f64]         ┆ f64   ┆ f64   ┆ f64   │
    #> ╞════════════╪═══════════════════╪═══════╪═══════╪═══════╡
    #> │ 2020-01-01 ┆ [3.0, 7.0, 5.0]   ┆ 15.0  ┆ 3.0   ┆ 7.0   │
    #> │ 2020-01-01 ┆ [3.0, 7.0, 5.0]   ┆ 15.0  ┆ 3.0   ┆ 7.0   │
    #> │ 2020-01-01 ┆ [3.0, 7.0, 5.0]   ┆ 15.0  ┆ 3.0   ┆ 7.0   │
    #> │ 2020-01-02 ┆ [3.0, 7.0, … 9.0] ┆ 24.0  ┆ 3.0   ┆ 9.0   │
    #> │ 2020-01-03 ┆ [9.0, 2.0]        ┆ 11.0  ┆ 2.0   ┆ 9.0   │
    #> │ 2020-01-08 ┆ [1.0]             ┆ 1.0   ┆ 1.0   ┆ 1.0   │
    #> └────────────┴───────────────────┴───────┴───────┴───────┘
