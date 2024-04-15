

# milliseconds

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__datetime.R#L828)

## Description

Extract the milliseconds from a Duration type.

## Usage

<pre><code class='language-R'>ExprDT_total_milliseconds()
</code></pre>

## Value

Expr of i64

## Examples

``` r
library(polars)

df = pl$DataFrame(date = pl$date_range(
  start = as.POSIXct("2020-1-1", tz = "GMT"),
  end = as.POSIXct("2020-1-1 00:00:01", tz = "GMT"),
  interval = "1ms"
))
df$select(
  pl$col("date"),
  diff_millisec = pl$col("date")$diff()$dt$total_milliseconds()
)
```

    #> shape: (1_001, 2)
    #> ┌─────────────────────────────┬───────────────┐
    #> │ date                        ┆ diff_millisec │
    #> │ ---                         ┆ ---           │
    #> │ datetime[ms, GMT]           ┆ i64           │
    #> ╞═════════════════════════════╪═══════════════╡
    #> │ 2020-01-01 00:00:00 GMT     ┆ null          │
    #> │ 2020-01-01 00:00:00.001 GMT ┆ 1             │
    #> │ 2020-01-01 00:00:00.002 GMT ┆ 1             │
    #> │ 2020-01-01 00:00:00.003 GMT ┆ 1             │
    #> │ 2020-01-01 00:00:00.004 GMT ┆ 1             │
    #> │ …                           ┆ …             │
    #> │ 2020-01-01 00:00:00.996 GMT ┆ 1             │
    #> │ 2020-01-01 00:00:00.997 GMT ┆ 1             │
    #> │ 2020-01-01 00:00:00.998 GMT ┆ 1             │
    #> │ 2020-01-01 00:00:00.999 GMT ┆ 1             │
    #> │ 2020-01-01 00:00:01 GMT     ┆ 1             │
    #> └─────────────────────────────┴───────────────┘
