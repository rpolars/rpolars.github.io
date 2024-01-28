

# nanoseconds

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__datetime.R#L878)

## Description

Extract the nanoseconds from a Duration type.

## Usage

<pre><code class='language-R'>ExprDT_total_nanoseconds()
</code></pre>

## Value

Expr of i64

## Examples

``` r
library(polars)

df = pl$DataFrame(date = pl$date_range(
  start = as.POSIXct("2020-1-1", tz = "GMT"),
  end = as.POSIXct("2020-1-1 00:00:01", tz = "GMT"),
  interval = "1ms",
  eager = TRUE
))
df$select(
  pl$col("date"),
  diff_nanosec = pl$col("date")$diff()$dt$total_nanoseconds()
)
```

    #> shape: (1_001, 2)
    #> ┌─────────────────────────────┬──────────────┐
    #> │ date                        ┆ diff_nanosec │
    #> │ ---                         ┆ ---          │
    #> │ datetime[μs, GMT]           ┆ i64          │
    #> ╞═════════════════════════════╪══════════════╡
    #> │ 2020-01-01 00:00:00 GMT     ┆ null         │
    #> │ 2020-01-01 00:00:00.001 GMT ┆ 1000000      │
    #> │ 2020-01-01 00:00:00.002 GMT ┆ 1000000      │
    #> │ 2020-01-01 00:00:00.003 GMT ┆ 1000000      │
    #> │ …                           ┆ …            │
    #> │ 2020-01-01 00:00:00.997 GMT ┆ 1000000      │
    #> │ 2020-01-01 00:00:00.998 GMT ┆ 1000000      │
    #> │ 2020-01-01 00:00:00.999 GMT ┆ 1000000      │
    #> │ 2020-01-01 00:00:01 GMT     ┆ 1000000      │
    #> └─────────────────────────────┴──────────────┘
