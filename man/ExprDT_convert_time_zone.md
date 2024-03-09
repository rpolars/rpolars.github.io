

# With Time Zone

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/expr__datetime.R#L701)

## Description

Set time zone for a Series of type Datetime. Use to change time zone
annotation, but keep the corresponding global timepoint.

## Usage

<pre><code class='language-R'>ExprDT_convert_time_zone(tz)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_convert_time_zone_:_tz">tz</code>
</td>
<td>
String time zone from base::OlsonNames()
</td>
</tr>
</table>

## Details

corresponds to in R manually modifying the tzone attribute of POSIXt
objects

## Value

Expr of i64

## Examples

``` r
library(polars)

df = pl$DataFrame(
  london_timezone = pl$date_range(
    as.POSIXct("2020-03-01", tz = "UTC"),
    as.POSIXct("2020-07-01", tz = "UTC"),
    "1mo",
    time_zone = "UTC"
  )$dt$convert_time_zone("Europe/London")
)

df$select(
  "london_timezone",
  London_to_Amsterdam = pl$col(
    "london_timezone"
  )$dt$replace_time_zone("Europe/Amsterdam")
)
```

    #> shape: (5, 2)
    #> ┌─────────────────────────────┬────────────────────────────────┐
    #> │ london_timezone             ┆ London_to_Amsterdam            │
    #> │ ---                         ┆ ---                            │
    #> │ datetime[μs, Europe/London] ┆ datetime[μs, Europe/Amsterdam] │
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

df = pl$DataFrame(
  ts = pl$Series(dates)$str$strptime(pl$Datetime("us"), "%F %H:%M"),
  ambiguous = c("earliest", "earliest", "latest", "latest")
)

df$with_columns(
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

``` r
# Polars Datetime type without a time zone will be converted to R
# with respect to the session time zone. If ambiguous times are present
# an error will be raised. It is recommended to add a time zone before
# converting to R.
s_without_tz = pl$Series(dates)$str$strptime(pl$Datetime("us"), "%F %H:%M")
s_without_tz
```

    #> polars Series: shape: (4,)
    #> Series: '' [datetime[μs]]
    #> [
    #>  2018-10-28 01:30:00
    #>  2018-10-28 02:00:00
    #>  2018-10-28 02:30:00
    #>  2018-10-28 02:00:00
    #> ]

``` r
s_with_tz = s_without_tz$dt$replace_time_zone("UTC")
s_with_tz
```

    #> polars Series: shape: (4,)
    #> Series: '' [datetime[μs, UTC]]
    #> [
    #>  2018-10-28 01:30:00 UTC
    #>  2018-10-28 02:00:00 UTC
    #>  2018-10-28 02:30:00 UTC
    #>  2018-10-28 02:00:00 UTC
    #> ]

``` r
as.vector(s_with_tz)
```

    #> [1] "2018-10-28 01:30:00 UTC" "2018-10-28 02:00:00 UTC"
    #> [3] "2018-10-28 02:30:00 UTC" "2018-10-28 02:00:00 UTC"
