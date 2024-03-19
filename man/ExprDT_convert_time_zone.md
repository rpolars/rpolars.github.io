

# Convert to given time zone for an expression of type Datetime.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__datetime.R#L664)

## Description

If converting from a time-zone-naive datetime, then conversion will
happen as if converting from UTC, regardless of your system’s time zone.

## Usage

<pre><code class='language-R'>ExprDT_convert_time_zone(time_zone)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_convert_time_zone_:_time_zone">time_zone</code>
</td>
<td>
String time zone from <code>base::OlsonNames()</code>
</td>
</tr>
</table>

## Value

Expr of i64

## Examples

``` r
library(polars)

df = pl$DataFrame(
  date = pl$date_range(
    as.POSIXct("2020-03-01", tz = "UTC"),
    as.POSIXct("2020-05-01", tz = "UTC"),
    "1mo"
  )
)

df$select(
  "date",
  London = pl$col("date")$dt$convert_time_zone("Europe/London")
)
```

    #> shape: (3, 2)
    #> ┌─────────────────────────┬─────────────────────────────┐
    #> │ date                    ┆ London                      │
    #> │ ---                     ┆ ---                         │
    #> │ datetime[μs, UTC]       ┆ datetime[μs, Europe/London] │
    #> ╞═════════════════════════╪═════════════════════════════╡
    #> │ 2020-03-01 00:00:00 UTC ┆ 2020-03-01 00:00:00 GMT     │
    #> │ 2020-04-01 00:00:00 UTC ┆ 2020-04-01 01:00:00 BST     │
    #> │ 2020-05-01 00:00:00 UTC ┆ 2020-05-01 01:00:00 BST     │
    #> └─────────────────────────┴─────────────────────────────┘
