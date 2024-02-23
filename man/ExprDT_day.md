

# Day

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__datetime.R#L343)

## Description

Extract day from underlying Date representation. Applies to Date and
Datetime columns. Returns the day of month starting from 1. The return
value ranges from 1 to 31. (The last day of month differs by months.)

## Usage

<pre><code class='language-R'>ExprDT_day()
</code></pre>

## Value

Expr of day as UInt32

## Examples

``` r
library(polars)

df = pl$DataFrame(
  date = pl$date_range(
    as.Date("2020-12-25"),
    as.Date("2021-1-05"),
    interval = "1d",
    time_zone = "GMT",
    eager = TRUE
  )
)
df$with_columns(
  pl$col("date")$dt$day()$alias("day")
)
```

    #> shape: (12, 2)
    #> ┌────────────┬─────┐
    #> │ date       ┆ day │
    #> │ ---        ┆ --- │
    #> │ date       ┆ i8  │
    #> ╞════════════╪═════╡
    #> │ 2020-12-25 ┆ 25  │
    #> │ 2020-12-26 ┆ 26  │
    #> │ 2020-12-27 ┆ 27  │
    #> │ 2020-12-28 ┆ 28  │
    #> │ 2020-12-29 ┆ 29  │
    #> │ …          ┆ …   │
    #> │ 2021-01-01 ┆ 1   │
    #> │ 2021-01-02 ┆ 2   │
    #> │ 2021-01-03 ┆ 3   │
    #> │ 2021-01-04 ┆ 4   │
    #> │ 2021-01-05 ┆ 5   │
    #> └────────────┴─────┘
