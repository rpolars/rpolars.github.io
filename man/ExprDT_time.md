
# Extract time from a Datetime Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__datetime.R#L1010)

## Description

This only works on Datetime Series, it will error on Date Series.

## Usage

<pre><code class='language-R'>ExprDT_time()
</code></pre>

## Value

A Time Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(dates = pl$date_range(
  as.Date("2000-1-1"),
  as.Date("2000-1-2"),
  "1h",
  eager = TRUE
))

df$with_columns(times = pl$col("dates")$dt$time())
```

    #> shape: (25, 2)
    #> ┌─────────────────────┬──────────┐
    #> │ dates               ┆ times    │
    #> │ ---                 ┆ ---      │
    #> │ datetime[μs]        ┆ time     │
    #> ╞═════════════════════╪══════════╡
    #> │ 2000-01-01 00:00:00 ┆ 00:00:00 │
    #> │ 2000-01-01 01:00:00 ┆ 01:00:00 │
    #> │ 2000-01-01 02:00:00 ┆ 02:00:00 │
    #> │ 2000-01-01 03:00:00 ┆ 03:00:00 │
    #> │ …                   ┆ …        │
    #> │ 2000-01-01 21:00:00 ┆ 21:00:00 │
    #> │ 2000-01-01 22:00:00 ┆ 22:00:00 │
    #> │ 2000-01-01 23:00:00 ┆ 23:00:00 │
    #> │ 2000-01-02 00:00:00 ┆ 00:00:00 │
    #> └─────────────────────┴──────────┘
