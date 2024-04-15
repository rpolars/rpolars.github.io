

# Generate a datetime range

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/functions__eager.R#L337)

## Description

Generate a datetime range

## Usage

<pre><code class='language-R'>pl_datetime_range(
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
<code id="pl_datetime_range_:_start">start</code>
</td>
<td>
Lower bound of the date range. Something that can be coerced to a Date
or a Datetime expression. See examples for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_range_:_end">end</code>
</td>
<td>
Upper bound of the date range. Something that can be coerced to a Date
or a Datetime expression. See examples for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_range_:_interval">interval</code>
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
<code id="pl_datetime_range_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_range_:_closed">closed</code>
</td>
<td>
Define which sides of the range are closed (inclusive). One of the
followings: <code>“both”</code> (default), <code>“left”</code>,
<code>“right”</code>, <code>“none”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_range_:_time_unit">time_unit</code>
</td>
<td>
Time unit of the resulting the Datetime data type. One of
<code>“ns”</code>, <code>“us”</code>, <code>“ms”</code> or
<code>NULL</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_range_:_time_zone">time_zone</code>
</td>
<td>
Time zone of the resulting Datetime data type.
</td>
</tr>
</table>

## Value

An Expr of data type Datetime

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

<code>pl$datetime_ranges()</code> to create a simple Series of data type
list(Datetime) based on column values.

## Examples

``` r
library(polars)

# Using Polars duration string to specify the interval:
pl$datetime_range(as.Date("2022-01-01"), as.Date("2022-03-01"), "1mo") |>
  as_polars_series("datetime")
```

    #> polars Series: shape: (3,)
    #> Series: 'datetime' [datetime[μs]]
    #> [
    #>  2022-01-01 00:00:00
    #>  2022-02-01 00:00:00
    #>  2022-03-01 00:00:00
    #> ]

``` r
# Using `difftime` object to specify the interval:
pl$datetime_range(
  as.Date("1985-01-01"),
  as.Date("1985-01-10"),
  as.difftime(1, units = "days") + as.difftime(12, units = "hours")
) |>
  as_polars_series("datetime")
```

    #> polars Series: shape: (7,)
    #> Series: 'datetime' [datetime[μs]]
    #> [
    #>  1985-01-01 00:00:00
    #>  1985-01-02 12:00:00
    #>  1985-01-04 00:00:00
    #>  1985-01-05 12:00:00
    #>  1985-01-07 00:00:00
    #>  1985-01-08 12:00:00
    #>  1985-01-10 00:00:00
    #> ]

``` r
# Specifying a time zone:
pl$datetime_range(
  as.Date("2022-01-01"),
  as.Date("2022-03-01"),
  "1mo",
  time_zone = "America/New_York"
) |>
  as_polars_series("datetime")
```

    #> polars Series: shape: (3,)
    #> Series: 'datetime' [datetime[μs, America/New_York]]
    #> [
    #>  2022-01-01 00:00:00 EST
    #>  2022-02-01 00:00:00 EST
    #>  2022-03-01 00:00:00 EST
    #> ]
