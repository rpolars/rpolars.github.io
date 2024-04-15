

# Truncate datetime

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__datetime.R#L36)

## Description

Divide the date/datetime range into buckets. Each date/datetime is
mapped to the start of its bucket.

## Usage

<pre><code class='language-R'>ExprDT_truncate(every, offset = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_truncate_:_every">every</code>
</td>
<td>
string encoding duration see details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_truncate_:_offset">offset</code>
</td>
<td>
optional string encoding duration see details.
</td>
</tr>
</table>

## Details

The <code>every</code> and <code>offset</code> argument are created with
the the following string language:

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

1y \# 1 calendar year These strings can be combined:

<ul>
<li>

3d12h4m25s \# 3 days, 12 hours, 4 minutes, and 25 seconds

</li>
</ul>
</li>
</ul>

## Value

Date/Datetime expr

## Examples

``` r
library(polars)

t1 = as.POSIXct("3040-01-01", tz = "GMT")
t2 = t1 + as.difftime(25, units = "secs")
s = pl$date_range(t1, t2, interval = "2s", time_unit = "ms")

# use a dt namespace function
df = pl$DataFrame(datetime = s)$with_columns(
  pl$col("datetime")$dt$truncate("4s")$alias("truncated_4s"),
  pl$col("datetime")$dt$truncate("4s", offset("3s"))$alias("truncated_4s_offset_2s")
)
df
```

    #> shape: (13, 3)
    #> ┌─────────────────────────┬─────────────────────────┬─────────────────────────┐
    #> │ datetime                ┆ truncated_4s            ┆ truncated_4s_offset_2s  │
    #> │ ---                     ┆ ---                     ┆ ---                     │
    #> │ datetime[ms, GMT]       ┆ datetime[ms, GMT]       ┆ datetime[ms, GMT]       │
    #> ╞═════════════════════════╪═════════════════════════╪═════════════════════════╡
    #> │ 3040-01-01 00:00:00 GMT ┆ 3040-01-01 00:00:00 GMT ┆ 3040-01-01 00:00:03 GMT │
    #> │ 3040-01-01 00:00:02 GMT ┆ 3040-01-01 00:00:00 GMT ┆ 3040-01-01 00:00:03 GMT │
    #> │ 3040-01-01 00:00:04 GMT ┆ 3040-01-01 00:00:04 GMT ┆ 3040-01-01 00:00:07 GMT │
    #> │ 3040-01-01 00:00:06 GMT ┆ 3040-01-01 00:00:04 GMT ┆ 3040-01-01 00:00:07 GMT │
    #> │ 3040-01-01 00:00:08 GMT ┆ 3040-01-01 00:00:08 GMT ┆ 3040-01-01 00:00:11 GMT │
    #> │ …                       ┆ …                       ┆ …                       │
    #> │ 3040-01-01 00:00:16 GMT ┆ 3040-01-01 00:00:16 GMT ┆ 3040-01-01 00:00:19 GMT │
    #> │ 3040-01-01 00:00:18 GMT ┆ 3040-01-01 00:00:16 GMT ┆ 3040-01-01 00:00:19 GMT │
    #> │ 3040-01-01 00:00:20 GMT ┆ 3040-01-01 00:00:20 GMT ┆ 3040-01-01 00:00:23 GMT │
    #> │ 3040-01-01 00:00:22 GMT ┆ 3040-01-01 00:00:20 GMT ┆ 3040-01-01 00:00:23 GMT │
    #> │ 3040-01-01 00:00:24 GMT ┆ 3040-01-01 00:00:24 GMT ┆ 3040-01-01 00:00:27 GMT │
    #> └─────────────────────────┴─────────────────────────┴─────────────────────────┘
