

# Replace time zone

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__datetime.R#L720)

## Description

Cast time zone for a Series of type Datetime. This is different from
<code>$convert_time_zone()</code> as it will also modify the underlying
timestamp. Use to correct a wrong time zone annotation. This will change
the corresponding global timepoint.

## Usage

<pre><code class='language-R'>ExprDT_replace_time_zone(
  time_zone,
  ...,
  ambiguous = "raise",
  non_existent = "raise"
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_replace_time_zone_:_time_zone">time_zone</code>
</td>
<td>
<code>NULL</code> or string time zone from
<code>base::OlsonNames()</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_replace_time_zone_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_replace_time_zone_:_ambiguous">ambiguous</code>
</td>
<td>

Determine how to deal with ambiguous datetimes:

<ul>
<li>

<code>“raise”</code> (default): throw an error

</li>
<li>

<code>“earliest”</code>: use the earliest datetime

</li>
<li>

<code>“latest”</code>: use the latest datetime

</li>
<li>

<code>“null”</code>: return a null value

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_replace_time_zone_:_non_existent">non_existent</code>
</td>
<td>

Determine how to deal with non-existent datetimes:

<ul>
<li>

<code>“raise”</code> (default): throw an error

</li>
<li>

<code>“null”</code>: return a null value

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr of i64

## Examples

``` r
library(polars)

df1 = pl$DataFrame(
  london_timezone = pl$date_range(
    as.POSIXct("2020-03-01", tz = "UTC"),
    as.POSIXct("2020-07-01", tz = "UTC"),
    "1mo"
  )$dt$convert_time_zone("Europe/London")
)

df1$select(
  "london_timezone",
  London_to_Amsterdam = pl$col("london_timezone")$dt$replace_time_zone("Europe/Amsterdam")
)
```

    #> shape: (5, 2)
    #> ┌─────────────────────────────┬────────────────────────────────┐
    #> │ london_timezone             ┆ London_to_Amsterdam            │
    #> │ ---                         ┆ ---                            │
    #> │ datetime[ms, Europe/London] ┆ datetime[ms, Europe/Amsterdam] │
    #> ╞═════════════════════════════╪════════════════════════════════╡
    #> │ 2020-03-01 00:00:00 GMT     ┆ 2020-03-01 00:00:00 CET        │
    #> │ 2020-04-01 01:00:00 BST     ┆ 2020-04-01 01:00:00 CEST       │
    #> │ 2020-05-01 01:00:00 BST     ┆ 2020-05-01 01:00:00 CEST       │
    #> │ 2020-06-01 01:00:00 BST     ┆ 2020-06-01 01:00:00 CEST       │
    #> │ 2020-07-01 01:00:00 BST     ┆ 2020-07-01 01:00:00 CEST       │
    #> └─────────────────────────────┴────────────────────────────────┘

``` r
# You can use `ambiguous` to deal with ambiguous datetimes:
dates = c(
  "2018-10-28 01:30",
  "2018-10-28 02:00",
  "2018-10-28 02:30",
  "2018-10-28 02:00"
)
df2 = pl$DataFrame(
  ts = as_polars_series(dates)$str$strptime(pl$Datetime("us")),
  ambiguous = c("earliest", "earliest", "latest", "latest")
)

df2$with_columns(
  ts_localized = pl$col("ts")$dt$replace_time_zone(
    "Europe/Brussels",
    ambiguous = pl$col("ambiguous")
  )
)
```

    #> shape: (4, 3)
    #> ┌─────────────────────┬───────────┬───────────────────────────────┐
    #> │ ts                  ┆ ambiguous ┆ ts_localized                  │
    #> │ ---                 ┆ ---       ┆ ---                           │
    #> │ datetime[μs]        ┆ str       ┆ datetime[μs, Europe/Brussels] │
    #> ╞═════════════════════╪═══════════╪═══════════════════════════════╡
    #> │ 2018-10-28 01:30:00 ┆ earliest  ┆ 2018-10-28 01:30:00 CEST      │
    #> │ 2018-10-28 02:00:00 ┆ earliest  ┆ 2018-10-28 02:00:00 CEST      │
    #> │ 2018-10-28 02:30:00 ┆ latest    ┆ 2018-10-28 02:30:00 CET       │
    #> │ 2018-10-28 02:00:00 ┆ latest    ┆ 2018-10-28 02:00:00 CET       │
    #> └─────────────────────┴───────────┴───────────────────────────────┘
