
# Minute

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__datetime.R#L451)

## Description

Extract minutes from underlying Datetime representation. Applies to
Datetime columns. Returns the minute number from 0 to 59.

## Format

function

## Value

Expr of minute as UInt32

## Examples

``` r
library(polars)

df = pl$DataFrame(
  date = pl$date_range(
    as.Date("2020-12-25"),
    as.Date("2021-1-05"),
    interval = "1d5s",
    time_zone = "GMT",
    eager = TRUE
  )
)
df$with_columns(
  pl$col("date")$dt$minute()$alias("minute")
)
```

    #> shape: (11, 2)
    #> ┌─────────────────────────┬────────┐
    #> │ date                    ┆ minute │
    #> │ ---                     ┆ ---    │
    #> │ datetime[μs, GMT]       ┆ i8     │
    #> ╞═════════════════════════╪════════╡
    #> │ 2020-12-25 00:00:00 GMT ┆ 0      │
    #> │ 2020-12-26 00:00:05 GMT ┆ 0      │
    #> │ 2020-12-27 00:00:10 GMT ┆ 0      │
    #> │ 2020-12-28 00:00:15 GMT ┆ 0      │
    #> │ …                       ┆ …      │
    #> │ 2021-01-01 00:00:35 GMT ┆ 0      │
    #> │ 2021-01-02 00:00:40 GMT ┆ 0      │
    #> │ 2021-01-03 00:00:45 GMT ┆ 0      │
    #> │ 2021-01-04 00:00:50 GMT ┆ 0      │
    #> └─────────────────────────┴────────┘
