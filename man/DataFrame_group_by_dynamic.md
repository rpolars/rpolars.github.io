

# Group based on a date/time or integer column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L2205)

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

<pre><code class='language-R'>DataFrame_group_by_dynamic(
  index_column,
  ...,
  every,
  period = NULL,
  offset = NULL,
  include_boundaries = FALSE,
  closed = "left",
  label = "left",
  group_by = NULL,
  start_by = "window",
  check_sorted = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="index_column">index_column</code>
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
<code id="...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="every">every</code>
</td>
<td>
Interval of the window.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="period">period</code>
</td>
<td>
A character representing the length of the window, must be non-negative.
See the <code style="white-space: pre;">Polars duration string
language</code> section for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="offset">offset</code>
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
<code id="include_boundaries">include_boundaries</code>
</td>
<td>
Add two columns <code>“\_lower_boundary”</code> and
<code>“\_upper_boundary”</code> columns that show the boundaries of the
window. This will impact performance because it’s harder to parallelize.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="closed">closed</code>
</td>
<td>
Define which sides of the temporal interval are closed (inclusive). This
can be either <code>“left”</code>, <code>“right”</code>,
<code>“both”</code> or <code>“none”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="label">label</code>
</td>
<td>

Define which label to use for the window:

<ul>
<li>

<code>“left”</code>: lower boundary of the window

</li>
<li>

<code>“right”</code>: upper boundary of the window

</li>
<li>

<code>“datapoint”</code>: the first value of the index column in the
given window. If you don’t need the label to be at one of the
boundaries, choose this option for maximum performance.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="group_by">group_by</code>
</td>
<td>
Also group by this column/these columns.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="start_by">start_by</code>
</td>
<td>

The strategy to determine the start of the first window by:

<ul>
<li>

<code>“window”</code>: start by taking the earliest timestamp,
truncating it with <code>every</code>, and then adding
<code>offset</code>. Note that weekly windows start on Monday.

</li>
<li>

<code>“datapoint”</code>: start from the first encountered data point.

</li>
<li>

a day of the week (only takes effect if <code>every</code> contains
<code>“w”</code>): <code>“monday”</code> starts the window on the Monday
before the first data point, etc.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="check_sorted">check_sorted</code>
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

A GroupBy object

## See Also

<ul>
<li>

<code>\<DataFrame\>$rolling()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  time = pl$datetime_range(
    start = strptime("2021-12-16 00:00:00", format = "%Y-%m-%d %H:%M:%S", tz = "UTC"),
    end = strptime("2021-12-16 03:00:00", format = "%Y-%m-%d %H:%M:%S", tz = "UTC"),
    interval = "30m"
  ),
  n = 0:6
)

# get the sum in the following hour relative to the "time" column
df$group_by_dynamic("time", every = "1h")$agg(
  vals = pl$col("n"),
  sum = pl$col("n")$sum()
)
```

    #> shape: (4, 3)
    #> ┌─────────────────────────┬───────────┬─────┐
    #> │ time                    ┆ vals      ┆ sum │
    #> │ ---                     ┆ ---       ┆ --- │
    #> │ datetime[ms, UTC]       ┆ list[i32] ┆ i32 │
    #> ╞═════════════════════════╪═══════════╪═════╡
    #> │ 2021-12-16 00:00:00 UTC ┆ [0, 1]    ┆ 1   │
    #> │ 2021-12-16 01:00:00 UTC ┆ [2, 3]    ┆ 5   │
    #> │ 2021-12-16 02:00:00 UTC ┆ [4, 5]    ┆ 9   │
    #> │ 2021-12-16 03:00:00 UTC ┆ [6]       ┆ 6   │
    #> └─────────────────────────┴───────────┴─────┘

``` r
# using "include_boundaries = TRUE" is helpful to see the period considered
df$group_by_dynamic("time", every = "1h", include_boundaries = TRUE)$agg(
  vals = pl$col("n")
)
```

    #> shape: (4, 4)
    #> ┌─────────────────────────┬─────────────────────────┬─────────────────────────┬───────────┐
    #> │ _lower_boundary         ┆ _upper_boundary         ┆ time                    ┆ vals      │
    #> │ ---                     ┆ ---                     ┆ ---                     ┆ ---       │
    #> │ datetime[ms, UTC]       ┆ datetime[ms, UTC]       ┆ datetime[ms, UTC]       ┆ list[i32] │
    #> ╞═════════════════════════╪═════════════════════════╪═════════════════════════╪═══════════╡
    #> │ 2021-12-16 00:00:00 UTC ┆ 2021-12-16 01:00:00 UTC ┆ 2021-12-16 00:00:00 UTC ┆ [0, 1]    │
    #> │ 2021-12-16 01:00:00 UTC ┆ 2021-12-16 02:00:00 UTC ┆ 2021-12-16 01:00:00 UTC ┆ [2, 3]    │
    #> │ 2021-12-16 02:00:00 UTC ┆ 2021-12-16 03:00:00 UTC ┆ 2021-12-16 02:00:00 UTC ┆ [4, 5]    │
    #> │ 2021-12-16 03:00:00 UTC ┆ 2021-12-16 04:00:00 UTC ┆ 2021-12-16 03:00:00 UTC ┆ [6]       │
    #> └─────────────────────────┴─────────────────────────┴─────────────────────────┴───────────┘

``` r
# in the example above, the values didn't include the one *exactly* 1h after
# the start because "closed = 'left'" by default.
# Changing it to "right" includes values that are exactly 1h after. Note that
# the value at 00:00:00 now becomes included in the interval [23:00:00 - 00:00:00],
# even if this interval wasn't there originally
df$group_by_dynamic("time", every = "1h", closed = "right")$agg(
  vals = pl$col("n")
)
```

    #> shape: (4, 2)
    #> ┌─────────────────────────┬───────────┐
    #> │ time                    ┆ vals      │
    #> │ ---                     ┆ ---       │
    #> │ datetime[ms, UTC]       ┆ list[i32] │
    #> ╞═════════════════════════╪═══════════╡
    #> │ 2021-12-15 23:00:00 UTC ┆ [0]       │
    #> │ 2021-12-16 00:00:00 UTC ┆ [1, 2]    │
    #> │ 2021-12-16 01:00:00 UTC ┆ [3, 4]    │
    #> │ 2021-12-16 02:00:00 UTC ┆ [5, 6]    │
    #> └─────────────────────────┴───────────┘

``` r
# To keep both boundaries, we use "closed = 'both'". Some values now belong to
# several groups:
df$group_by_dynamic("time", every = "1h", closed = "both")$agg(
  vals = pl$col("n")
)
```

    #> shape: (5, 2)
    #> ┌─────────────────────────┬───────────┐
    #> │ time                    ┆ vals      │
    #> │ ---                     ┆ ---       │
    #> │ datetime[ms, UTC]       ┆ list[i32] │
    #> ╞═════════════════════════╪═══════════╡
    #> │ 2021-12-15 23:00:00 UTC ┆ [0]       │
    #> │ 2021-12-16 00:00:00 UTC ┆ [0, 1, 2] │
    #> │ 2021-12-16 01:00:00 UTC ┆ [2, 3, 4] │
    #> │ 2021-12-16 02:00:00 UTC ┆ [4, 5, 6] │
    #> │ 2021-12-16 03:00:00 UTC ┆ [6]       │
    #> └─────────────────────────┴───────────┘

``` r
# Dynamic group bys can also be combined with grouping on normal keys
df = df$with_columns(
  groups = as_polars_series(c("a", "a", "a", "b", "b", "a", "a"))
)
df
```

    #> shape: (7, 3)
    #> ┌─────────────────────────┬─────┬────────┐
    #> │ time                    ┆ n   ┆ groups │
    #> │ ---                     ┆ --- ┆ ---    │
    #> │ datetime[ms, UTC]       ┆ i32 ┆ str    │
    #> ╞═════════════════════════╪═════╪════════╡
    #> │ 2021-12-16 00:00:00 UTC ┆ 0   ┆ a      │
    #> │ 2021-12-16 00:30:00 UTC ┆ 1   ┆ a      │
    #> │ 2021-12-16 01:00:00 UTC ┆ 2   ┆ a      │
    #> │ 2021-12-16 01:30:00 UTC ┆ 3   ┆ b      │
    #> │ 2021-12-16 02:00:00 UTC ┆ 4   ┆ b      │
    #> │ 2021-12-16 02:30:00 UTC ┆ 5   ┆ a      │
    #> │ 2021-12-16 03:00:00 UTC ┆ 6   ┆ a      │
    #> └─────────────────────────┴─────┴────────┘

``` r
df$group_by_dynamic(
  "time",
  every = "1h",
  closed = "both",
  group_by = "groups",
  include_boundaries = TRUE
)$agg(pl$col("n"))
```

    #> shape: (7, 5)
    #> ┌────────┬─────────────────────────┬─────────────────────────┬─────────────────────────┬───────────┐
    #> │ groups ┆ _lower_boundary         ┆ _upper_boundary         ┆ time                    ┆ n         │
    #> │ ---    ┆ ---                     ┆ ---                     ┆ ---                     ┆ ---       │
    #> │ str    ┆ datetime[ms, UTC]       ┆ datetime[ms, UTC]       ┆ datetime[ms, UTC]       ┆ list[i32] │
    #> ╞════════╪═════════════════════════╪═════════════════════════╪═════════════════════════╪═══════════╡
    #> │ a      ┆ 2021-12-15 23:00:00 UTC ┆ 2021-12-16 00:00:00 UTC ┆ 2021-12-15 23:00:00 UTC ┆ [0]       │
    #> │ a      ┆ 2021-12-16 00:00:00 UTC ┆ 2021-12-16 01:00:00 UTC ┆ 2021-12-16 00:00:00 UTC ┆ [0, 1, 2] │
    #> │ a      ┆ 2021-12-16 01:00:00 UTC ┆ 2021-12-16 02:00:00 UTC ┆ 2021-12-16 01:00:00 UTC ┆ [2]       │
    #> │ a      ┆ 2021-12-16 02:00:00 UTC ┆ 2021-12-16 03:00:00 UTC ┆ 2021-12-16 02:00:00 UTC ┆ [5, 6]    │
    #> │ a      ┆ 2021-12-16 03:00:00 UTC ┆ 2021-12-16 04:00:00 UTC ┆ 2021-12-16 03:00:00 UTC ┆ [6]       │
    #> │ b      ┆ 2021-12-16 01:00:00 UTC ┆ 2021-12-16 02:00:00 UTC ┆ 2021-12-16 01:00:00 UTC ┆ [3, 4]    │
    #> │ b      ┆ 2021-12-16 02:00:00 UTC ┆ 2021-12-16 03:00:00 UTC ┆ 2021-12-16 02:00:00 UTC ┆ [4]       │
    #> └────────┴─────────────────────────┴─────────────────────────┴─────────────────────────┴───────────┘

``` r
# We can also create a dynamic group by based on an index column
df = pl$LazyFrame(
  idx = 0:5,
  A = c("A", "A", "B", "B", "B", "C")
)$with_columns(pl$col("idx")$set_sorted())
df
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #>  WITH_COLUMNS:
    #>  [col("idx").map()]
    #>   DF ["idx", "A"]; PROJECT */2 COLUMNS; SELECTION: "None"

``` r
df$group_by_dynamic(
  "idx",
  every = "2i",
  period = "3i",
  include_boundaries = TRUE,
  closed = "right"
)$agg(A_agg_list = pl$col("A"))
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> AGGREGATE
    #>  [col("A").alias("A_agg_list")] BY [] FROM
    #>    WITH_COLUMNS:
    #>    [col("idx").map()]
    #>     DF ["idx", "A"]; PROJECT */2 COLUMNS; SELECTION: "None"
