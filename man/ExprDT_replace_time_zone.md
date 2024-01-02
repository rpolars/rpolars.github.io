
# replace_time_zone

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__datetime.R#L775)

## Description

Cast time zone for a Series of type Datetime. Different from
<code>convert_time_zone</code>, this will also modify the underlying
timestamp. Use to correct a wrong time zone annotation. This will change
the corresponding global timepoint.

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_replace_time_zone_:_tz">tz</code>
</td>
<td>
NULL or string time zone from <code>base::OlsonNames()</code>
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

## Format

function

## Value

Expr of i64

## Examples

``` r
library(polars)

df_1 = pl$DataFrame(x = as.POSIXct("2009-08-07 00:00:01", tz = "America/New_York"))

df_1$with_columns(
  pl$col("x")$dt$replace_time_zone("UTC")$alias("utc"),
  pl$col("x")$dt$replace_time_zone("Europe/Amsterdam")$alias("cest")
)
```

    #> shape: (1, 3)
    #> ┌────────────────────────────────┬─────────────────────────┬────────────────────────────────┐
    #> │ x                              ┆ utc                     ┆ cest                           │
    #> │ ---                            ┆ ---                     ┆ ---                            │
    #> │ datetime[ms, America/New_York] ┆ datetime[ms, UTC]       ┆ datetime[ms, Europe/Amsterdam] │
    #> ╞════════════════════════════════╪═════════════════════════╪════════════════════════════════╡
    #> │ 2009-08-07 00:00:01 EDT        ┆ 2009-08-07 00:00:01 UTC ┆ 2009-08-07 00:00:01 CEST       │
    #> └────────────────────────────────┴─────────────────────────┴────────────────────────────────┘

``` r
# You can use ambiguous to deal with ambiguous datetimes
df_2 = pl$DataFrame(
  x = seq(
    as.POSIXct("2018-10-28 01:30", tz = "UTC"),
    as.POSIXct("2018-10-28 02:30", tz = "UTC"),
    by = "30 min"
  )
)

df_2$with_columns(
  pl$col("x")$dt$replace_time_zone("Europe/Brussels", "earliest")$alias("earliest"),
  pl$col("x")$dt$replace_time_zone("Europe/Brussels", "latest")$alias("latest")
)
```

    #> shape: (3, 3)
    #> ┌─────────────────────────┬───────────────────────────────┬───────────────────────────────┐
    #> │ x                       ┆ earliest                      ┆ latest                        │
    #> │ ---                     ┆ ---                           ┆ ---                           │
    #> │ datetime[ms, UTC]       ┆ datetime[ms, Europe/Brussels] ┆ datetime[ms, Europe/Brussels] │
    #> ╞═════════════════════════╪═══════════════════════════════╪═══════════════════════════════╡
    #> │ 2018-10-28 01:30:00 UTC ┆ 2018-10-28 01:30:00 CEST      ┆ 2018-10-28 01:30:00 CEST      │
    #> │ 2018-10-28 02:00:00 UTC ┆ 2018-10-28 02:00:00 CEST      ┆ 2018-10-28 02:00:00 CET       │
    #> │ 2018-10-28 02:30:00 UTC ┆ 2018-10-28 02:30:00 CEST      ┆ 2018-10-28 02:30:00 CET       │
    #> └─────────────────────────┴───────────────────────────────┴───────────────────────────────┘
