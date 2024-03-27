

# Create rolling groups based on a date/time or integer column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L2013)

## Description

If you have a time series <code style="white-space: pre;">\<t_0, t_1, …,
t_n\></code>, then by default the windows created will be:

<ul>
<li>

(t_0 - period, t_0\]

</li>
<li>

(t_1 - period, t_1\]

</li>
<li>

…

</li>
<li>

(t_n - period, t_n\]

</li>
</ul>

whereas if you pass a non-default offset, then the windows will be:

<ul>
<li>

(t_0 + offset, t_0 + offset + period\]

</li>
<li>

(t_1 + offset, t_1 + offset + period\]

</li>
<li>

…

</li>
<li>

(t_n + offset, t_n + offset + period\]

</li>
</ul>

## Usage

<pre><code class='language-R'>DataFrame_rolling(
  index_column,
  period,
  offset = NULL,
  closed = "right",
  by = NULL,
  check_sorted = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_rolling_:_index_column">index_column</code>
</td>
<td>
Column used to group based on the time window. Often of type
Date/Datetime. This column must be sorted in ascending order (or, if
<code>by</code> is specified, then it must be sorted in ascending order
within each group). In case of a rolling group by on indices, dtype
needs to be either Int32 or Int64. Note that Int32 gets temporarily cast
to Int64, so if performance matters use an Int64 column.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_rolling_:_period">period</code>
</td>
<td>
A character representing the length of the window, must be non-negative.
See the <code style="white-space: pre;">Polars duration string
language</code> section for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_rolling_:_offset">offset</code>
</td>
<td>
A character representing the offset of the window, or <code>NULL</code>
(default). If <code>NULL</code>, <code>-period</code> is used. See the
<code style="white-space: pre;">Polars duration string language</code>
section for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_rolling_:_closed">closed</code>
</td>
<td>
Define which sides of the temporal interval are closed (inclusive). This
can be either <code>“left”</code>, <code>“right”</code>,
<code>“both”</code> or <code>“none”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_rolling_:_by">by</code>
</td>
<td>
Also group by this column/these columns.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_rolling_:_check_sorted">check_sorted</code>
</td>
<td>
Check whether data is actually sorted. Checking it is expensive so if
you are sure the data within the <code>index_column</code> is sorted,
you can set this to <code>FALSE</code> but note that if the data
actually is unsorted, it will lead to incorrect output.
</td>
</tr>
</table>

## Details

In case of a rolling operation on an integer column, the windows are
defined by:

<ul>
<li>

"1i" \# length 1

</li>
<li>

"10i" \# length 10

</li>
</ul>

## Value

A RollingGroupBy object

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
