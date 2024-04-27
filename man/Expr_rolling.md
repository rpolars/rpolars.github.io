

# Create rolling groups based on a time or numeric column

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L3327)

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

<pre><code class='language-R'>Expr_rolling(
  index_column,
  ...,
  period,
  offset = NULL,
  closed = "right",
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
Date/Datetime. This column must be sorted in ascending order. If this
column represents an index, it has to be either Int32 or Int64. Note
that Int32 gets temporarily cast to Int64, so if performance matters use
an Int64 column.
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

Expr

## Polars duration string language

Polars duration string language is a simple representation of durations.
It is used in many Polars functions that accept durations.

It has the following format:

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
</ul>

Or combine them: <code>“3d12h4m25s”</code> \# 3 days, 12 hours, 4
minutes, and 25 seconds

By "calendar day", we mean the corresponding time on the next day (which
may not be 24 hours, due to daylight savings). Similarly for "calendar
week", "calendar month", "calendar quarter", and "calendar year".

## Examples

``` r
library(polars)

# create a DataFrame with a Datetime column and an f64 column
dates = c(
  "2020-01-01 13:45:48", "2020-01-01 16:42:13", "2020-01-01 16:45:09",
  "2020-01-02 18:12:48", "2020-01-03 19:45:32", "2020-01-08 23:16:43"
)

df = pl$DataFrame(dt = dates, a = c(3, 7, 5, 9, 2, 1))$
  with_columns(
  pl$col("dt")$str$strptime(pl$Datetime("us"), format = "%Y-%m-%d %H:%M:%S")$set_sorted()
)

df$with_columns(
  sum_a = pl$sum("a")$rolling(index_column = "dt", period = "2d"),
  min_a = pl$min("a")$rolling(index_column = "dt", period = "2d"),
  max_a = pl$max("a")$rolling(index_column = "dt", period = "2d")
)
```

    #> shape: (6, 5)
    #> ┌─────────────────────┬─────┬───────┬───────┬───────┐
    #> │ dt                  ┆ a   ┆ sum_a ┆ min_a ┆ max_a │
    #> │ ---                 ┆ --- ┆ ---   ┆ ---   ┆ ---   │
    #> │ datetime[μs]        ┆ f64 ┆ f64   ┆ f64   ┆ f64   │
    #> ╞═════════════════════╪═════╪═══════╪═══════╪═══════╡
    #> │ 2020-01-01 13:45:48 ┆ 3.0 ┆ 3.0   ┆ 3.0   ┆ 3.0   │
    #> │ 2020-01-01 16:42:13 ┆ 7.0 ┆ 10.0  ┆ 3.0   ┆ 7.0   │
    #> │ 2020-01-01 16:45:09 ┆ 5.0 ┆ 15.0  ┆ 3.0   ┆ 7.0   │
    #> │ 2020-01-02 18:12:48 ┆ 9.0 ┆ 24.0  ┆ 3.0   ┆ 9.0   │
    #> │ 2020-01-03 19:45:32 ┆ 2.0 ┆ 11.0  ┆ 2.0   ┆ 9.0   │
    #> │ 2020-01-08 23:16:43 ┆ 1.0 ┆ 1.0   ┆ 1.0   ┆ 1.0   │
    #> └─────────────────────┴─────┴───────┴───────┴───────┘

``` r
# we can use "offset" to change the start of the window period. Here, with
# offset = "1d", we start the window one day after the value in "dt", and
# then we add a 2-day window relative to the window start.
df$with_columns(
  sum_a_offset1 = pl$sum("a")$rolling(index_column = "dt", period = "2d", offset = "1d")
)
```

    #> shape: (6, 3)
    #> ┌─────────────────────┬─────┬───────────────┐
    #> │ dt                  ┆ a   ┆ sum_a_offset1 │
    #> │ ---                 ┆ --- ┆ ---           │
    #> │ datetime[μs]        ┆ f64 ┆ f64           │
    #> ╞═════════════════════╪═════╪═══════════════╡
    #> │ 2020-01-01 13:45:48 ┆ 3.0 ┆ 11.0          │
    #> │ 2020-01-01 16:42:13 ┆ 7.0 ┆ 11.0          │
    #> │ 2020-01-01 16:45:09 ┆ 5.0 ┆ 11.0          │
    #> │ 2020-01-02 18:12:48 ┆ 9.0 ┆ 2.0           │
    #> │ 2020-01-03 19:45:32 ┆ 2.0 ┆ null          │
    #> │ 2020-01-08 23:16:43 ┆ 1.0 ┆ null          │
    #> └─────────────────────┴─────┴───────────────┘
