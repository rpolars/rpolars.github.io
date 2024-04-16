

# Generate a list containing a date range

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/functions__eager.R#L286)

## Description

If both <code>start</code> and <code>end</code> are passed as the Date
types (not Datetime), and the <code>interval</code> granularity is no
finer than <code>“1d”</code>, the returned range is also of type Date.
All other permutations return a Datetime. Note that in a future version
of Polars, <code>pl$date_ranges()</code> will always return Date. Please
use <code>pl$datetime_ranges()</code> if you want Datetime instead.

## Usage

<pre><code class='language-R'>pl_date_ranges(
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
<code id="pl_date_ranges_:_start">start</code>
</td>
<td>
Lower bound of the date range. Something that can be coerced to a Date
or a Datetime expression. See examples for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_ranges_:_end">end</code>
</td>
<td>
Upper bound of the date range. Something that can be coerced to a Date
or a Datetime expression. See examples for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_ranges_:_interval">interval</code>
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
<code id="pl_date_ranges_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_ranges_:_closed">closed</code>
</td>
<td>
Define which sides of the range are closed (inclusive). One of the
followings: <code>“both”</code> (default), <code>“left”</code>,
<code>“right”</code>, <code>“none”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_ranges_:_time_unit">time_unit</code>
</td>
<td>
Time unit of the resulting the Datetime data type. One of
<code>“ns”</code>, <code>“us”</code>, <code>“ms”</code> or
<code>NULL</code>. Only takes effect if the output column is of type
Datetime (deprecated usage).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_ranges_:_time_zone">time_zone</code>
</td>
<td>
Time zone of the resulting Datetime data type. Only takes effect if the
output column is of type Datetime (deprecated usage).
</td>
</tr>
</table>

## Value

An Expr of data type List(Date) or List(Datetime)

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

<code>pl$date_range()</code> to create a simple Series of data type
Date.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  start = as.Date(c("2022-01-01", "2022-01-02", NA)),
  end = as.Date("2022-01-03")
)

df$with_columns(
  date_range = pl$date_ranges("start", "end"),
  date_range_cr = pl$date_ranges("start", "end", closed = "right")
)
```

    #> shape: (3, 4)
    #> ┌────────────┬────────────┬───────────────────────────────────┬──────────────────────────┐
    #> │ start      ┆ end        ┆ date_range                        ┆ date_range_cr            │
    #> │ ---        ┆ ---        ┆ ---                               ┆ ---                      │
    #> │ date       ┆ date       ┆ list[date]                        ┆ list[date]               │
    #> ╞════════════╪════════════╪═══════════════════════════════════╪══════════════════════════╡
    #> │ 2022-01-01 ┆ 2022-01-03 ┆ [2022-01-01, 2022-01-02, 2022-01… ┆ [2022-01-02, 2022-01-03] │
    #> │ 2022-01-02 ┆ 2022-01-03 ┆ [2022-01-02, 2022-01-03]          ┆ [2022-01-03]             │
    #> │ null       ┆ 2022-01-03 ┆ null                              ┆ null                     │
    #> └────────────┴────────────┴───────────────────────────────────┴──────────────────────────┘

``` r
# provide a custom "end" value
df$with_columns(
  date_range_lit = pl$date_ranges("start", pl$lit(as.Date("2022-01-02")))
)
```

    #> shape: (3, 3)
    #> ┌────────────┬────────────┬──────────────────────────┐
    #> │ start      ┆ end        ┆ date_range_lit           │
    #> │ ---        ┆ ---        ┆ ---                      │
    #> │ date       ┆ date       ┆ list[date]               │
    #> ╞════════════╪════════════╪══════════════════════════╡
    #> │ 2022-01-01 ┆ 2022-01-03 ┆ [2022-01-01, 2022-01-02] │
    #> │ 2022-01-02 ┆ 2022-01-03 ┆ [2022-01-02]             │
    #> │ null       ┆ 2022-01-03 ┆ null                     │
    #> └────────────┴────────────┴──────────────────────────┘
