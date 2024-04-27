

# Offset By

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__datetime.R#L927)

## Description

Offset this date by a relative time offset. This differs from
<code>pl$col(“foo_datetime_tu”) + value_tu</code> in that it can take
months and leap years into account. Note that only a single minus sign
is allowed in the <code>by</code> string, as the first character.

## Usage

<pre><code class='language-R'>ExprDT_offset_by(by)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="by">by</code>
</td>
<td>
optional string encoding duration see details.
</td>
</tr>
</table>

## Details

The <code>by</code> are created with the the following string language:

<ul>
<li>

1ns \# 1 nanosecond

</li>
<li>

1us \# 1 microsecond

</li>
<li>

1ms \# 1 millisecond

</li>
<li>

1s \# 1 second

</li>
<li>

1m \# 1 minute

</li>
<li>

1h \# 1 hour

</li>
<li>

1d \# 1 day

</li>
<li>

1w \# 1 calendar week

</li>
<li>

1mo \# 1 calendar month

</li>
<li>

1y \# 1 calendar year

</li>
<li>

1i \# 1 index count

</li>
</ul>

These strings can be combined:

<ul>
<li>

3d12h4m25s \# 3 days, 12 hours, 4 minutes, and 25 seconds

</li>
</ul>

## Value

Date/Datetime expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  dates = pl$date_range(
    as.Date("2000-1-1"),
    as.Date("2005-1-1"),
    "1y"
  )
)
df$select(
  pl$col("dates")$dt$offset_by("1y")$alias("date_plus_1y"),
  pl$col("dates")$dt$offset_by("-1y2mo")$alias("date_min")
)
```

    #> shape: (6, 2)
    #> ┌──────────────┬────────────┐
    #> │ date_plus_1y ┆ date_min   │
    #> │ ---          ┆ ---        │
    #> │ date         ┆ date       │
    #> ╞══════════════╪════════════╡
    #> │ 2001-01-01   ┆ 1998-11-01 │
    #> │ 2002-01-01   ┆ 1999-11-01 │
    #> │ 2003-01-01   ┆ 2000-11-01 │
    #> │ 2004-01-01   ┆ 2001-11-01 │
    #> │ 2005-01-01   ┆ 2002-11-01 │
    #> │ 2006-01-01   ┆ 2003-11-01 │
    #> └──────────────┴────────────┘

``` r
# the "by" argument also accepts expressions
df = pl$DataFrame(
  dates = pl$date_range(
    as.POSIXct("2022-01-01", tz = "GMT"),
    as.POSIXct("2022-01-02", tz = "GMT"),
    interval = "6h", time_unit = "ms", time_zone = "GMT"
  )$to_r(),
  offset = c("1d", "-2d", "1mo", NA, "1y")
)

df
```

    #> shape: (5, 2)
    #> ┌─────────────────────────┬────────┐
    #> │ dates                   ┆ offset │
    #> │ ---                     ┆ ---    │
    #> │ datetime[ms, GMT]       ┆ str    │
    #> ╞═════════════════════════╪════════╡
    #> │ 2022-01-01 00:00:00 GMT ┆ 1d     │
    #> │ 2022-01-01 06:00:00 GMT ┆ -2d    │
    #> │ 2022-01-01 12:00:00 GMT ┆ 1mo    │
    #> │ 2022-01-01 18:00:00 GMT ┆ null   │
    #> │ 2022-01-02 00:00:00 GMT ┆ 1y     │
    #> └─────────────────────────┴────────┘

``` r
df$with_columns(new_dates = pl$col("dates")$dt$offset_by(pl$col("offset")))
```

    #> shape: (5, 3)
    #> ┌─────────────────────────┬────────┬─────────────────────────┐
    #> │ dates                   ┆ offset ┆ new_dates               │
    #> │ ---                     ┆ ---    ┆ ---                     │
    #> │ datetime[ms, GMT]       ┆ str    ┆ datetime[ms, GMT]       │
    #> ╞═════════════════════════╪════════╪═════════════════════════╡
    #> │ 2022-01-01 00:00:00 GMT ┆ 1d     ┆ 2022-01-02 00:00:00 GMT │
    #> │ 2022-01-01 06:00:00 GMT ┆ -2d    ┆ 2021-12-30 06:00:00 GMT │
    #> │ 2022-01-01 12:00:00 GMT ┆ 1mo    ┆ 2022-02-01 12:00:00 GMT │
    #> │ 2022-01-01 18:00:00 GMT ┆ null   ┆ null                    │
    #> │ 2022-01-02 00:00:00 GMT ┆ 1y     ┆ 2023-01-02 00:00:00 GMT │
    #> └─────────────────────────┴────────┴─────────────────────────┘
