

# Replace time zone

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__datetime.R#L749)

## Description

Cast time zone for a Series of type Datetime. This is different from
<code>$convert_time_zone()</code> as it will also modify the underlying
timestamp. Use to correct a wrong time zone annotation. This will change
the corresponding global timepoint.

## Usage

<pre><code class='language-R'>ExprDT_replace_time_zone(tz, ambiguous = "raise", non_existent = "raise")
</code></pre>

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
  pl$col("x")$dt$replace_time_zone("Europe/Brussels", "latest")$alias("latest"),
  pl$col("x")$dt$replace_time_zone("Europe/Brussels", "null")$alias("null")
)
```

    #> shape: (3, 4)
    #> ┌────────────────────────┬────────────────────────┬────────────────────────┬───────────────────────┐
    #> │ x                      ┆ earliest               ┆ latest                 ┆ null                  │
    #> │ ---                    ┆ ---                    ┆ ---                    ┆ ---                   │
    #> │ datetime[ms, UTC]      ┆ datetime[ms,           ┆ datetime[ms,           ┆ datetime[ms,          │
    #> │                        ┆ Europe/Brussels]       ┆ Europe/Brussels]       ┆ Europe/Brussels]      │
    #> ╞════════════════════════╪════════════════════════╪════════════════════════╪═══════════════════════╡
    #> │ 2018-10-28 01:30:00    ┆ 2018-10-28 01:30:00    ┆ 2018-10-28 01:30:00    ┆ 2018-10-28 01:30:00   │
    #> │ UTC                    ┆ CEST                   ┆ CEST                   ┆ CEST                  │
    #> │ 2018-10-28 02:00:00    ┆ 2018-10-28 02:00:00    ┆ 2018-10-28 02:00:00    ┆ null                  │
    #> │ UTC                    ┆ CEST                   ┆ CET                    ┆                       │
    #> │ 2018-10-28 02:30:00    ┆ 2018-10-28 02:30:00    ┆ 2018-10-28 02:30:00    ┆ null                  │
    #> │ UTC                    ┆ CEST                   ┆ CET                    ┆                       │
    #> └────────────────────────┴────────────────────────┴────────────────────────┴───────────────────────┘
