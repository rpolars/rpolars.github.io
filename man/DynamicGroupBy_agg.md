

# Aggregate over a DynamicGroupBy

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/group_by_dynamic.R#L91)

## Description

Aggregate a DataFrame over a time or integer window created with
<code style="white-space: pre;">$group_by_dynamic()</code>.

## Usage

<pre><code class='language-R'>DynamicGroupBy_agg(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DynamicGroupBy_agg_:_...">…</code>
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
  time = pl$date_range(
    start = strptime("2021-12-16 00:00:00", format = "%Y-%m-%d %H:%M:%S", tz = "UTC"),
    end = strptime("2021-12-16 03:00:00", format = "%Y-%m-%d %H:%M:%S", tz = "UTC"),
    interval = "30m",
    eager = TRUE,
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
    #> │ datetime[μs, UTC]       ┆ list[i32] ┆ i32 │
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
df$group_by_dynamic("time", every = "1h", closed = "right")$agg(
  vals = pl$col("n")
)
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
df$group_by_dynamic("time", every = "1h", closed = "both")$agg(
  vals = pl$col("n")
)
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
df = df$with_columns(groups = pl$Series(c("a", "a", "a", "b", "b", "a", "a")))
df
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
df$group_by_dynamic(
  "time",
  every = "1h",
  closed = "both",
  by = "groups",
  include_boundaries = TRUE
)$agg(pl$col("n"))
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
df = pl$LazyFrame(
  idx = 0:5,
  A = c("A", "A", "B", "B", "B", "C")
)$with_columns(pl$col("idx")$set_sorted())
df
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
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

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> AGGREGATE
    #>  [col("A").alias("A_agg_list")] BY [] FROM
    #>    WITH_COLUMNS:
    #>    [col("idx").map()]
    #>     DF ["idx", "A"]; PROJECT */2 COLUMNS; SELECTION: "None"
