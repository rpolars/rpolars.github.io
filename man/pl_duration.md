

# Create polars Duration from distinct time components

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L1024)

## Description

Create polars Duration from distinct time components

## Usage

<pre><code class='language-R'>pl_duration(
  ...,
  weeks = NULL,
  days = NULL,
  hours = NULL,
  minutes = NULL,
  seconds = NULL,
  milliseconds = NULL,
  microseconds = NULL,
  nanoseconds = NULL,
  time_unit = "us"
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_weeks">weeks</code>
</td>
<td>
Number of weeks to add. Expr or something coercible to an Expr. Strings
are parsed as column names. <em>Same thing for argument
<code>days</code> to <code>nanoseconds</code></em>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_days">days</code>
</td>
<td>
Number of days to add.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_hours">hours</code>
</td>
<td>
Number of hours to add.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_minutes">minutes</code>
</td>
<td>
Number of minutes to add.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_seconds">seconds</code>
</td>
<td>
Number of seconds to add.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_milliseconds">milliseconds</code>
</td>
<td>
Number of milliseconds to add.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_microseconds">microseconds</code>
</td>
<td>
Number of microseconds to add.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_nanoseconds">nanoseconds</code>
</td>
<td>
Number of nanoseconds to add.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_duration_:_time_unit">time_unit</code>
</td>
<td>
Time unit of the resulting expression.
</td>
</tr>
</table>

## Details

A duration represents a fixed amount of time. For example,
<code>pl$duration(days = 1)</code> means "exactly 24 hours". By
contrast, <code>Expr$dt$offset_by(‘1d’)</code> means "1 calendar day",
which could sometimes be 23 hours or 25 hours depending on Daylight
Savings Time. For non-fixed durations such as "calendar month" or
"calendar day", please use <code>Expr$dt$offset_by()</code> instead.

## Value

Expr

## Examples

``` r
library(polars)

test = pl$DataFrame(
  dt = c(
    "2022-01-01 00:00:00",
    "2022-01-02 00:00:00"
  ),
  add = 1:2
)$with_columns(
  pl$col("dt")$str$strptime(pl$Datetime("us"), format = NULL)
)

test$with_columns(
  (pl$col("dt") + pl$duration(weeks = "add"))$alias("add_weeks"),
  (pl$col("dt") + pl$duration(days = "add"))$alias("add_days"),
  (pl$col("dt") + pl$duration(seconds = "add"))$alias("add_seconds"),
  (pl$col("dt") + pl$duration(milliseconds = "add"))$alias("add_millis"),
  (pl$col("dt") + pl$duration(hours = "add"))$alias("add_hours")
)
```

    #> shape: (2, 7)
    #> ┌───────────────┬─────┬───────────────┬───────────────┬──────────────┬──────────────┬──────────────┐
    #> │ dt            ┆ add ┆ add_weeks     ┆ add_days      ┆ add_seconds  ┆ add_millis   ┆ add_hours    │
    #> │ ---           ┆ --- ┆ ---           ┆ ---           ┆ ---          ┆ ---          ┆ ---          │
    #> │ datetime[μs]  ┆ i32 ┆ datetime[μs]  ┆ datetime[μs]  ┆ datetime[μs] ┆ datetime[μs] ┆ datetime[μs] │
    #> ╞═══════════════╪═════╪═══════════════╪═══════════════╪══════════════╪══════════════╪══════════════╡
    #> │ 2022-01-01    ┆ 1   ┆ 2022-01-08    ┆ 2022-01-02    ┆ 2022-01-01   ┆ 2022-01-01   ┆ 2022-01-01   │
    #> │ 00:00:00      ┆     ┆ 00:00:00      ┆ 00:00:00      ┆ 00:00:01     ┆ 00:00:00.001 ┆ 01:00:00     │
    #> │ 2022-01-02    ┆ 2   ┆ 2022-01-16    ┆ 2022-01-04    ┆ 2022-01-02   ┆ 2022-01-02   ┆ 2022-01-02   │
    #> │ 00:00:00      ┆     ┆ 00:00:00      ┆ 00:00:00      ┆ 00:00:02     ┆ 00:00:00.002 ┆ 02:00:00     │
    #> └───────────────┴─────┴───────────────┴───────────────┴──────────────┴──────────────┴──────────────┘

``` r
# we can also pass an Expr
test$with_columns(
  (pl$col("dt") + pl$duration(weeks = pl$col("add") + 1))$alias("add_weeks"),
  (pl$col("dt") + pl$duration(days = pl$col("add") + 1))$alias("add_days"),
  (pl$col("dt") + pl$duration(seconds = pl$col("add") + 1))$alias("add_seconds"),
  (pl$col("dt") + pl$duration(milliseconds = pl$col("add") + 1))$alias("add_millis"),
  (pl$col("dt") + pl$duration(hours = pl$col("add") + 1))$alias("add_hours")
)
```

    #> shape: (2, 7)
    #> ┌───────────────┬─────┬───────────────┬───────────────┬──────────────┬──────────────┬──────────────┐
    #> │ dt            ┆ add ┆ add_weeks     ┆ add_days      ┆ add_seconds  ┆ add_millis   ┆ add_hours    │
    #> │ ---           ┆ --- ┆ ---           ┆ ---           ┆ ---          ┆ ---          ┆ ---          │
    #> │ datetime[μs]  ┆ i32 ┆ datetime[μs]  ┆ datetime[μs]  ┆ datetime[μs] ┆ datetime[μs] ┆ datetime[μs] │
    #> ╞═══════════════╪═════╪═══════════════╪═══════════════╪══════════════╪══════════════╪══════════════╡
    #> │ 2022-01-01    ┆ 1   ┆ 2022-01-15    ┆ 2022-01-03    ┆ 2022-01-01   ┆ 2022-01-01   ┆ 2022-01-01   │
    #> │ 00:00:00      ┆     ┆ 00:00:00      ┆ 00:00:00      ┆ 00:00:02     ┆ 00:00:00.002 ┆ 02:00:00     │
    #> │ 2022-01-02    ┆ 2   ┆ 2022-01-23    ┆ 2022-01-05    ┆ 2022-01-02   ┆ 2022-01-02   ┆ 2022-01-02   │
    #> │ 00:00:00      ┆     ┆ 00:00:00      ┆ 00:00:00      ┆ 00:00:03     ┆ 00:00:00.003 ┆ 03:00:00     │
    #> └───────────────┴─────┴───────────────┴───────────────┴──────────────┴──────────────┴──────────────┘
