

# With Time Zone

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__datetime.R#L686)

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
  date = pl$date_range(
    start = as.Date("2001-3-1"),
    end = as.Date("2001-5-1"),
    interval = "1mo12m34s",
    eager = TRUE
  )
)
df$select(
  pl$col("date"),
  pl$col("date")
  $dt$replace_time_zone("Europe/Amsterdam")
  $dt$convert_time_zone("Europe/London")
  $alias("London_with")
)
```

    #> shape: (2, 2)
    #> ┌─────────────────────┬─────────────────────────────┐
    #> │ date                ┆ London_with                 │
    #> │ ---                 ┆ ---                         │
    #> │ datetime[μs]        ┆ datetime[μs, Europe/London] │
    #> ╞═════════════════════╪═════════════════════════════╡
    #> │ 2001-03-01 00:00:00 ┆ 2001-02-28 23:00:00 GMT     │
    #> │ 2001-04-01 00:12:34 ┆ 2001-03-31 23:12:34 BST     │
    #> └─────────────────────┴─────────────────────────────┘
