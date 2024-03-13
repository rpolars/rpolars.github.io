

# Create a Datetime expression

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L1110)

## Description

Create a Datetime expression

## Usage

<pre><code class='language-R'>pl_datetime(
  year,
  month,
  day,
  hour = NULL,
  minute = NULL,
  second = NULL,
  microsecond = NULL,
  ...,
  time_unit = "us",
  time_zone = NULL,
  ambiguous = "raise"
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_year">year</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer.
Strings are parsed as column names. Floats are cast to integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_month">month</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 1 and 12. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_day">day</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 1 and 31. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_hour">hour</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 0 and 23. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_minute">minute</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 0 and 59. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_second">second</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 0 and 59. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_microsecond">microsecond</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 0 and 999,999. Strings are parsed as column names. Floats are
cast to integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_time_unit">time_unit</code>
</td>
<td>
Unit of time. One of <code>“ms”</code>, <code>“us”</code> (default) or
<code>“ns”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_time_zone">time_zone</code>
</td>
<td>
Time zone string, as defined in <code>OlsonNames()</code>. Setting
<code>timezone = “\*“</code> will match any timezone, which can be
useful to select all Datetime columns containing a timezone.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_datetime_:_ambiguous">ambiguous</code>
</td>
<td>

Determine how to deal with ambiguous datetimes:

<ul>
<li>

<code>“raise”</code> (default): raise

</li>
<li>

<code>“earliest”</code>: use the earliest datetime

</li>
<li>

<code>“latest”</code>: use the latest datetime

</li>
</ul>
</td>
</tr>
</table>

## Value

An Expr of type Datetime

## See Also

<ul>
<li>

<code>pl$date()</code>

</li>
<li>

<code>pl$time()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  year = 2019:2021,
  month = 9:11,
  day = 10:12,
  min = 55:57
)

df$with_columns(
  dt_from_cols = pl$datetime("year", "month", "day", minute = "min"),
  dt_from_lit = pl$datetime(2020, 3, 5, hour = 20:22),
  dt_from_mix = pl$datetime("year", 3, 5, second = 1)
)
```

    #> shape: (3, 7)
    #> ┌──────┬───────┬─────┬─────┬─────────────────────┬─────────────────────┬─────────────────────┐
    #> │ year ┆ month ┆ day ┆ min ┆ dt_from_cols        ┆ dt_from_lit         ┆ dt_from_mix         │
    #> │ ---  ┆ ---   ┆ --- ┆ --- ┆ ---                 ┆ ---                 ┆ ---                 │
    #> │ i32  ┆ i32   ┆ i32 ┆ i32 ┆ datetime[μs]        ┆ datetime[μs]        ┆ datetime[μs]        │
    #> ╞══════╪═══════╪═════╪═════╪═════════════════════╪═════════════════════╪═════════════════════╡
    #> │ 2019 ┆ 9     ┆ 10  ┆ 55  ┆ 2019-09-10 00:55:00 ┆ 2020-03-05 20:00:00 ┆ 2019-03-05 00:00:01 │
    #> │ 2020 ┆ 10    ┆ 11  ┆ 56  ┆ 2020-10-11 00:56:00 ┆ 2020-03-05 21:00:00 ┆ 2020-03-05 00:00:01 │
    #> │ 2021 ┆ 11    ┆ 12  ┆ 57  ┆ 2021-11-12 00:57:00 ┆ 2020-03-05 22:00:00 ┆ 2021-03-05 00:00:01 │
    #> └──────┴───────┴─────┴─────┴─────────────────────┴─────────────────────┴─────────────────────┘

``` r
# floats are coerced to integers
df$with_columns(
  dt_floats = pl$datetime(2018.8, 5.3, 1, second = 2.1)
)
```

    #> shape: (3, 5)
    #> ┌──────┬───────┬─────┬─────┬─────────────────────┐
    #> │ year ┆ month ┆ day ┆ min ┆ dt_floats           │
    #> │ ---  ┆ ---   ┆ --- ┆ --- ┆ ---                 │
    #> │ i32  ┆ i32   ┆ i32 ┆ i32 ┆ datetime[μs]        │
    #> ╞══════╪═══════╪═════╪═════╪═════════════════════╡
    #> │ 2019 ┆ 9     ┆ 10  ┆ 55  ┆ 2018-05-01 00:00:02 │
    #> │ 2020 ┆ 10    ┆ 11  ┆ 56  ┆ 2018-05-01 00:00:02 │
    #> │ 2021 ┆ 11    ┆ 12  ┆ 57  ┆ 2018-05-01 00:00:02 │
    #> └──────┴───────┴─────┴─────┴─────────────────────┘

``` r
# if datetime can't be constructed, it returns null
df$with_columns(
  dt_floats = pl$datetime(pl$lit("abc"), -2, 1)
)
```

    #> shape: (3, 5)
    #> ┌──────┬───────┬─────┬─────┬──────────────┐
    #> │ year ┆ month ┆ day ┆ min ┆ dt_floats    │
    #> │ ---  ┆ ---   ┆ --- ┆ --- ┆ ---          │
    #> │ i32  ┆ i32   ┆ i32 ┆ i32 ┆ datetime[μs] │
    #> ╞══════╪═══════╪═════╪═════╪══════════════╡
    #> │ 2019 ┆ 9     ┆ 10  ┆ 55  ┆ null         │
    #> │ 2020 ┆ 10    ┆ 11  ┆ 56  ┆ null         │
    #> │ 2021 ┆ 11    ┆ 12  ┆ 57  ┆ null         │
    #> └──────┴───────┴─────┴─────┴──────────────┘

``` r
# can control the time_unit
df$with_columns(
  dt_from_cols = pl$datetime("year", "month", "day", minute = "min", time_unit = "ms")
)
```

    #> shape: (3, 5)
    #> ┌──────┬───────┬─────┬─────┬─────────────────────┐
    #> │ year ┆ month ┆ day ┆ min ┆ dt_from_cols        │
    #> │ ---  ┆ ---   ┆ --- ┆ --- ┆ ---                 │
    #> │ i32  ┆ i32   ┆ i32 ┆ i32 ┆ datetime[ms]        │
    #> ╞══════╪═══════╪═════╪═════╪═════════════════════╡
    #> │ 2019 ┆ 9     ┆ 10  ┆ 55  ┆ 2019-09-10 00:55:00 │
    #> │ 2020 ┆ 10    ┆ 11  ┆ 56  ┆ 2020-10-11 00:56:00 │
    #> │ 2021 ┆ 11    ┆ 12  ┆ 57  ┆ 2021-11-12 00:57:00 │
    #> └──────┴───────┴─────┴─────┴─────────────────────┘
