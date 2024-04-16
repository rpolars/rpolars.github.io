

# Generate a list containing a datetime range

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__eager.R#L378)

## Description

Generate a list containing a datetime range

## Usage

<pre><code class='language-R'>pl_datetime_ranges(
  start,
  end,
  interval = "1d",
  ...,
  closed = "both",
  time_unit = NULL,
  time_zone = NULL
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_ranges_:_start">start</code>
</td>
<td>
Lower bound of the date range. Something that can be coerced to a Date
or a Datetime expression. See examples for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_ranges_:_end">end</code>
</td>
<td>
Upper bound of the date range. Something that can be coerced to a Date
or a Datetime expression. See examples for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_ranges_:_interval">interval</code>
</td>
<td>
Interval of the range periods, specified as a difftime object or using
the Polars duration string language. See the
<code style="white-space: pre;">Polars duration string language</code>
section for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_ranges_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_ranges_:_closed">closed</code>
</td>
<td>
Define which sides of the range are closed (inclusive). One of the
followings: <code>“both”</code> (default), <code>“left”</code>,
<code>“right”</code>, <code>“none”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_ranges_:_time_unit">time_unit</code>
</td>
<td>
Time unit of the resulting the Datetime data type. One of
<code>“ns”</code>, <code>“us”</code>, <code>“ms”</code> or
<code>NULL</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_ranges_:_time_zone">time_zone</code>
</td>
<td>
Time zone of the resulting Datetime data type.
</td>
</tr>
</table>

## Value

An Expr of data type list(Datetime)

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

## See Also

<code>pl$datetime_range()</code> to create a simple Series of data type
Datetime.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  start = as.POSIXct(c("2022-01-01 10:00", "2022-01-01 11:00", NA)),
  end = as.POSIXct("2022-01-01 12:00")
)

df$with_columns(
  dt_range = pl$datetime_ranges("start", "end", interval = "1h"),
  dt_range_cr = pl$datetime_ranges("start", "end", closed = "right", interval = "1h")
)
```

    #> shape: (3, 4)
    #> ┌─────────────────────┬─────────────────────┬───────────────────────┬───────────────────────┐
    #> │ start               ┆ end                 ┆ dt_range              ┆ dt_range_cr           │
    #> │ ---                 ┆ ---                 ┆ ---                   ┆ ---                   │
    #> │ datetime[ms]        ┆ datetime[ms]        ┆ list[datetime[ms]]    ┆ list[datetime[ms]]    │
    #> ╞═════════════════════╪═════════════════════╪═══════════════════════╪═══════════════════════╡
    #> │ 2022-01-01 10:00:00 ┆ 2022-01-01 12:00:00 ┆ [2022-01-01 10:00:00, ┆ [2022-01-01 11:00:00, │
    #> │                     ┆                     ┆ 2022-01-01…           ┆ 2022-01-01…           │
    #> │ 2022-01-01 11:00:00 ┆ 2022-01-01 12:00:00 ┆ [2022-01-01 11:00:00, ┆ [2022-01-01 12:00:00] │
    #> │                     ┆                     ┆ 2022-01-01…           ┆                       │
    #> │ null                ┆ 2022-01-01 12:00:00 ┆ null                  ┆ null                  │
    #> └─────────────────────┴─────────────────────┴───────────────────────┴───────────────────────┘

``` r
# provide a custom "end" value
df$with_columns(
  dt_range_lit = pl$datetime_ranges(
    "start", pl$lit(as.POSIXct("2022-01-01 11:00")),
    interval = "1h"
  )
)
```

    #> shape: (3, 3)
    #> ┌─────────────────────┬─────────────────────┬───────────────────────────────────┐
    #> │ start               ┆ end                 ┆ dt_range_lit                      │
    #> │ ---                 ┆ ---                 ┆ ---                               │
    #> │ datetime[ms]        ┆ datetime[ms]        ┆ list[datetime[ms]]                │
    #> ╞═════════════════════╪═════════════════════╪═══════════════════════════════════╡
    #> │ 2022-01-01 10:00:00 ┆ 2022-01-01 12:00:00 ┆ [2022-01-01 10:00:00, 2022-01-01… │
    #> │ 2022-01-01 11:00:00 ┆ 2022-01-01 12:00:00 ┆ [2022-01-01 11:00:00]             │
    #> │ null                ┆ 2022-01-01 12:00:00 ┆ null                              │
    #> └─────────────────────┴─────────────────────┴───────────────────────────────────┘
