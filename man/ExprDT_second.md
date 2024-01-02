
# Second

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__datetime.R#L479)

## Description

Extract seconds from underlying Datetime representation. Applies to
Datetime columns. Returns the integer second number from 0 to 59, or a
floating point number from 0 \< 60 if <code>fractional=True</code> that
includes any milli/micro/nanosecond component.

## Format

function

## Value

Expr of second as UInt32

## Examples

``` r
library(polars)

pl$DataFrame(date = pl$date_range(
  as.numeric(as.POSIXct("2001-1-1")) * 1E6 + 456789, # manually convert to us
  as.numeric(as.POSIXct("2001-1-1 00:00:6")) * 1E6,
  interval = "2s654321us",
  time_unit = "us", # instruct polars input is us, and store as us
  eager = TRUE
))$with_columns(
  pl$col("date")$dt$second()$alias("second"),
  pl$col("date")$dt$second(fractional = TRUE)$alias("second_frac")
)
```

    #> shape: (2_089, 3)
    #> ┌──────────────────────────────┬────────┬─────────────┐
    #> │ date                         ┆ second ┆ second_frac │
    #> │ ---                          ┆ ---    ┆ ---         │
    #> │ datetime[μs]                 ┆ i8     ┆ f64         │
    #> ╞══════════════════════════════╪════════╪═════════════╡
    #> │ +32971-04-28 00:07:36.789    ┆ 36     ┆ 36.789      │
    #> │ +32971-04-28 00:07:39.443321 ┆ 39     ┆ 39.443321   │
    #> │ +32971-04-28 00:07:42.097642 ┆ 42     ┆ 42.097642   │
    #> │ +32971-04-28 00:07:44.751963 ┆ 44     ┆ 44.751963   │
    #> │ …                            ┆ …      ┆ …           │
    #> │ +32971-04-28 01:39:51.048285 ┆ 51     ┆ 51.048285   │
    #> │ +32971-04-28 01:39:53.702606 ┆ 53     ┆ 53.702606   │
    #> │ +32971-04-28 01:39:56.356927 ┆ 56     ┆ 56.356927   │
    #> │ +32971-04-28 01:39:59.011248 ┆ 59     ┆ 59.011248   │
    #> └──────────────────────────────┴────────┴─────────────┘
