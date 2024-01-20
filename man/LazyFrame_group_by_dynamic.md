
# Group based on a date/time or integer column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1851)

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

<pre><code class='language-R'>LazyFrame_group_by_dynamic(
  index_column,
  ...,
  every,
  period = NULL,
  offset = NULL,
  include_boundaries = FALSE,
  closed = "left",
  label = "left",
  by = NULL,
  start_by = "window",
  check_sorted = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_dynamic_:_index_column">index_column</code>
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
<code id="LazyFrame_group_by_dynamic_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_dynamic_:_every">every</code>
</td>
<td>
Interval of the window.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_dynamic_:_period">period</code>
</td>
<td>
Length of the window, must be non-negative.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_dynamic_:_offset">offset</code>
</td>
<td>
Offset of the window. Default is <code>-period</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_dynamic_:_include_boundaries">include_boundaries</code>
</td>
<td>
Add two columns <code>“\_lower_boundary”</code> and
<code>“\_upper_boundary”</code> columns that show the boundaries of the
window. This will impact performance because it’s harder to parallelize.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_dynamic_:_closed">closed</code>
</td>
<td>
Define which sides of the temporal interval are closed (inclusive). This
can be either <code>“left”</code>, <code>“right”</code>,
<code>“both”</code> or <code>“none”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_dynamic_:_label">label</code>
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
<code id="LazyFrame_group_by_dynamic_:_by">by</code>
</td>
<td>
Also group by this column/these columns.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_dynamic_:_start_by">start_by</code>
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
<code id="LazyFrame_group_by_dynamic_:_check_sorted">check_sorted</code>
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

The period and offset arguments are created either from a timedelta, or
by using the following string language:

<ul>
<li>

1ns (1 nanosecond)

</li>
<li>

1us (1 microsecond)

</li>
<li>

1ms (1 millisecond)

</li>
<li>

1s (1 second)

</li>
<li>

1m (1 minute)

</li>
<li>

1h (1 hour)

</li>
<li>

1d (1 calendar day)

</li>
<li>

1w (1 calendar week)

</li>
<li>

1mo (1 calendar month)

</li>
<li>

1q (1 calendar quarter)

</li>
<li>

1y (1 calendar year)

</li>
<li>

1i (1 index count)

</li>
</ul>

Or combine them: "3d12h4m25s" \# 3 days, 12 hours, 4 minutes, and 25
seconds

By "calendar day", we mean the corresponding time on the next day (which
may not be 24 hours, due to daylight savings). Similarly for "calendar
week", "calendar month", "calendar quarter", and "calendar year".

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

A LazyGroupBy object

## Examples

``` r
library(polars)

lf = pl$LazyFrame(
  time = pl$date_range(
    start = strptime("2021-12-16 00:00:00", format = "%Y-%m-%d %H:%M:%S", tz = "UTC"),
    end = strptime("2021-12-16 03:00:00", format = "%Y-%m-%d %H:%M:%S", tz = "UTC"),
    interval = "30m",
    eager = TRUE,
  ),
  n = 0:6
)
lf$collect()
```

    #> shape: (7, 2)
    #> ┌─────────────────────────┬─────┐
    #> │ time                    ┆ n   │
    #> │ ---                     ┆ --- │
    #> │ datetime[μs, UTC]       ┆ i32 │
    #> ╞═════════════════════════╪═════╡
    #> │ 2021-12-16 00:00:00 UTC ┆ 0   │
    #> │ 2021-12-16 00:30:00 UTC ┆ 1   │
    #> │ 2021-12-16 01:00:00 UTC ┆ 2   │
    #> │ 2021-12-16 01:30:00 UTC ┆ 3   │
    #> │ 2021-12-16 02:00:00 UTC ┆ 4   │
    #> │ 2021-12-16 02:30:00 UTC ┆ 5   │
    #> │ 2021-12-16 03:00:00 UTC ┆ 6   │
    #> └─────────────────────────┴─────┘

``` r
# get the sum in the following hour relative to the "time" column
lf$group_by_dynamic("time", every = "1h")$agg(
  vals = pl$col("n"),
  sum = pl$col("n")$sum()
)$collect()
```

    #> shape: (4, 3)
    #> ┌─────────────────────────┬───────────┬─────┐
    #> │ time                    ┆ vals      ┆ sum │
    #> │ ---                     ┆ ---       ┆ --- │
    #> │ datetime[μs, UTC]       ┆ list[i32] ┆ i32 │
    #> ╞═════════════════════════╪═══════════╪═════╡
    #> │ 2021-12-16 00:00:00 UTC ┆ [0, 1]    ┆ 1   │
    #> │ 2021-12-16 01:00:00 UTC ┆ [2, 3]    ┆ 5   │
    #> │ 2021-12-16 02:00:00 UTC ┆ [4, 5]    ┆ 9   │
    #> │ 2021-12-16 03:00:00 UTC ┆ [6]       ┆ 6   │
    #> └─────────────────────────┴───────────┴─────┘

``` r
# using "include_boundaries = TRUE" is helpful to see the period considered
lf$group_by_dynamic("time", every = "1h", include_boundaries = TRUE)$agg(
  vals = pl$col("n")
)$collect()
```

    #> shape: (4, 4)
    #> ┌─────────────────────────┬─────────────────────────┬─────────────────────────┬───────────┐
    #> │ _lower_boundary         ┆ _upper_boundary         ┆ time                    ┆ vals      │
    #> │ ---                     ┆ ---                     ┆ ---                     ┆ ---       │
    #> │ datetime[μs, UTC]       ┆ datetime[μs, UTC]       ┆ datetime[μs, UTC]       ┆ list[i32] │
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
lf$group_by_dynamic("time", every = "1h", closed = "right")$agg(
  vals = pl$col("n")
)$collect()
```

    #> shape: (4, 2)
    #> ┌─────────────────────────┬───────────┐
    #> │ time                    ┆ vals      │
    #> │ ---                     ┆ ---       │
    #> │ datetime[μs, UTC]       ┆ list[i32] │
    #> ╞═════════════════════════╪═══════════╡
    #> │ 2021-12-15 23:00:00 UTC ┆ [0]       │
    #> │ 2021-12-16 00:00:00 UTC ┆ [1, 2]    │
    #> │ 2021-12-16 01:00:00 UTC ┆ [3, 4]    │
    #> │ 2021-12-16 02:00:00 UTC ┆ [5, 6]    │
    #> └─────────────────────────┴───────────┘

``` r
# To keep both boundaries, we use "closed = 'both'". Some values now belong to
# several groups:
lf$group_by_dynamic("time", every = "1h", closed = "both")$agg(
  vals = pl$col("n")
)$collect()
```

    #> shape: (5, 2)
    #> ┌─────────────────────────┬───────────┐
    #> │ time                    ┆ vals      │
    #> │ ---                     ┆ ---       │
    #> │ datetime[μs, UTC]       ┆ list[i32] │
    #> ╞═════════════════════════╪═══════════╡
    #> │ 2021-12-15 23:00:00 UTC ┆ [0]       │
    #> │ 2021-12-16 00:00:00 UTC ┆ [0, 1, 2] │
    #> │ 2021-12-16 01:00:00 UTC ┆ [2, 3, 4] │
    #> │ 2021-12-16 02:00:00 UTC ┆ [4, 5, 6] │
    #> │ 2021-12-16 03:00:00 UTC ┆ [6]       │
    #> └─────────────────────────┴───────────┘

``` r
# Dynamic group bys can also be combined with grouping on normal keys
lf = lf$with_columns(groups = pl$Series(c("a", "a", "a", "b", "b", "a", "a")))
lf$collect()
```

    #> shape: (7, 3)
    #> ┌─────────────────────────┬─────┬────────┐
    #> │ time                    ┆ n   ┆ groups │
    #> │ ---                     ┆ --- ┆ ---    │
    #> │ datetime[μs, UTC]       ┆ i32 ┆ str    │
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
lf$group_by_dynamic(
  "time",
  every = "1h",
  closed = "both",
  by = "groups",
  include_boundaries = TRUE
)$agg(pl$col("n"))$collect()
```

    #> shape: (7, 5)
    #> ┌────────┬─────────────────────────┬─────────────────────────┬─────────────────────────┬───────────┐
    #> │ groups ┆ _lower_boundary         ┆ _upper_boundary         ┆ time                    ┆ n         │
    #> │ ---    ┆ ---                     ┆ ---                     ┆ ---                     ┆ ---       │
    #> │ str    ┆ datetime[μs, UTC]       ┆ datetime[μs, UTC]       ┆ datetime[μs, UTC]       ┆ list[i32] │
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
lf = pl$LazyFrame(
  idx = 0:5,
  A = c("A", "A", "B", "B", "B", "C")
)$with_columns(pl$col("idx")$set_sorted())
lf$collect()
```

    #> shape: (6, 2)
    #> ┌─────┬─────┐
    #> │ idx ┆ A   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ str │
    #> ╞═════╪═════╡
    #> │ 0   ┆ A   │
    #> │ 1   ┆ A   │
    #> │ 2   ┆ B   │
    #> │ 3   ┆ B   │
    #> │ 4   ┆ B   │
    #> │ 5   ┆ C   │
    #> └─────┴─────┘

``` r
lf$group_by_dynamic(
  "idx",
  every = "2i",
  period = "3i",
  include_boundaries = TRUE,
  closed = "right"
)$agg(A_agg_list = pl$col("A"))$collect()
```

    #> shape: (4, 4)
    #> ┌─────────────────┬─────────────────┬─────┬─────────────────┐
    #> │ _lower_boundary ┆ _upper_boundary ┆ idx ┆ A_agg_list      │
    #> │ ---             ┆ ---             ┆ --- ┆ ---             │
    #> │ i32             ┆ i32             ┆ i32 ┆ list[str]       │
    #> ╞═════════════════╪═════════════════╪═════╪═════════════════╡
    #> │ -2              ┆ 1               ┆ -2  ┆ ["A", "A"]      │
    #> │ 0               ┆ 3               ┆ 0   ┆ ["A", "B", "B"] │
    #> │ 2               ┆ 5               ┆ 2   ┆ ["B", "B", "C"] │
    #> │ 4               ┆ 7               ┆ 4   ┆ ["C"]           │
    #> └─────────────────┴─────────────────┴─────┴─────────────────┘
