
# Millisecond

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__datetime.R#L509)

## Description

Extract milliseconds from underlying Datetime representation. Applies to
Datetime columns.

## Format

function

## Value

Expr of millisecond as Int64

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
  pl$col("date")$cast(pl$Int64)$alias("datetime int64"),
  pl$col("date")$dt$millisecond()$alias("millisecond")
)
```

    #> shape: (2_089, 3)
    #> ┌──────────────────────────────┬────────────────────┬─────────────┐
    #> │ date                         ┆ datetime int64     ┆ millisecond │
    #> │ ---                          ┆ ---                ┆ ---         │
    #> │ datetime[μs]                 ┆ i64                ┆ i32         │
    #> ╞══════════════════════════════╪════════════════════╪═════════════╡
    #> │ +32971-04-28 00:07:36.789    ┆ 978307200456789000 ┆ 789         │
    #> │ +32971-04-28 00:07:39.443321 ┆ 978307200459443321 ┆ 443         │
    #> │ +32971-04-28 00:07:42.097642 ┆ 978307200462097642 ┆ 97          │
    #> │ +32971-04-28 00:07:44.751963 ┆ 978307200464751963 ┆ 751         │
    #> │ …                            ┆ …                  ┆ …           │
    #> │ +32971-04-28 01:39:51.048285 ┆ 978307205991048285 ┆ 48          │
    #> │ +32971-04-28 01:39:53.702606 ┆ 978307205993702606 ┆ 702         │
    #> │ +32971-04-28 01:39:56.356927 ┆ 978307205996356927 ┆ 356         │
    #> │ +32971-04-28 01:39:59.011248 ┆ 978307205999011248 ┆ 11          │
    #> └──────────────────────────────┴────────────────────┴─────────────┘
