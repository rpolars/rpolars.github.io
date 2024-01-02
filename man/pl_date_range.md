
# New date range

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/functions__eager.R#L217)

## Description

New date range

## Usage

<pre><code class='language-R'>pl_date_range(
  start,
  end,
  interval,
  eager = FALSE,
  closed = "both",
  time_unit = "us",
  time_zone = NULL,
  explode = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_range_:_start">start</code>
</td>
<td>
POSIXt or Date preferably with time_zone or double or integer
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_range_:_end">end</code>
</td>
<td>
POSIXt or Date preferably with time_zone or double or integer. If
<code>end</code> and <code>interval</code> are missing, then a single
datetime is constructed.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_range_:_interval">interval</code>
</td>
<td>
String, a Polars <code>duration</code> or R <code>difftime()</code>. Can
be missing if <code>end</code> is missing also.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_range_:_eager">eager</code>
</td>
<td>
If <code>FALSE</code> (default), return an <code>Expr</code>. Otherwise,
returns a <code>Series</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_range_:_closed">closed</code>
</td>
<td>
One of <code>“both”</code> (default), <code>“left”</code>,
<code>“none”</code> or <code>“right”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_range_:_time_unit">time_unit</code>
</td>
<td>
String (<code>“ns”</code>, <code>“us”</code>, <code>“ms”</code>) or
integer.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_range_:_time_zone">time_zone</code>
</td>
<td>
String describing a timezone. If <code>NULL</code> (default),
<code style="white-space: pre;">“GMT</code> is used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_date_range_:_explode">explode</code>
</td>
<td>
If <code>TRUE</code> (default), all created ranges will be "unlisted"
into a column. Otherwise, output will be a list of ranges.
</td>
</tr>
</table>

## Details

If param <code>time_zone</code> is not defined the Series will have no
time zone.

Note that R POSIXt without defined timezones (tzone/tz), so-called naive
datetimes, are counter intuitive in R. It is recommended to always set
the timezone of start and end. If not output will vary between local
machine timezone, R and polars.

In R/r-polars it is perfectly fine to mix timezones of params
<code>time_zone</code>, <code>start</code> and <code>end</code>.

## Value

A datetime

## Examples

``` r
library(polars)

# All in GMT, straight forward, no mental confusion
s_gmt = pl$date_range(
  as.POSIXct("2022-01-01", tz = "GMT"),
  as.POSIXct("2022-01-02", tz = "GMT"),
  interval = "6h", time_unit = "ms", time_zone = "GMT"
)
s_gmt
```

    #> polars Expr: Series.date_range([Series]).explode()

``` r
s_gmt$to_r()
```

    #> [1] "2022-01-01 00:00:00 GMT" "2022-01-01 06:00:00 GMT"
    #> [3] "2022-01-01 12:00:00 GMT" "2022-01-01 18:00:00 GMT"
    #> [5] "2022-01-02 00:00:00 GMT"

``` r
# polars uses "GMT" if time_zone = NULL
s_null = pl$date_range(
  as.POSIXct("2022-01-01", tz = "GMT"),
  as.POSIXct("2022-01-02", tz = "GMT"),
  interval = "6h", time_unit = "ms", time_zone = NULL
)
# back to R POSIXct. R prints non tzone tagged POSIXct in local timezone
s_null$to_r()
```

    #> [1] "2022-01-01 00:00:00 GMT" "2022-01-01 06:00:00 GMT"
    #> [3] "2022-01-01 12:00:00 GMT" "2022-01-01 18:00:00 GMT"
    #> [5] "2022-01-02 00:00:00 GMT"

``` r
# use of ISOdate
t1 = ISOdate(2022, 1, 1, 0) # preset GMT
t2 = ISOdate(2022, 1, 2, 0) # preset GMT
pl$date_range(t1, t2, interval = "4h", time_unit = "ms", time_zone = "GMT")$to_r()
```

    #> [1] "2022-01-01 00:00:00 GMT" "2022-01-01 04:00:00 GMT"
    #> [3] "2022-01-01 08:00:00 GMT" "2022-01-01 12:00:00 GMT"
    #> [5] "2022-01-01 16:00:00 GMT" "2022-01-01 20:00:00 GMT"
    #> [7] "2022-01-02 00:00:00 GMT"
