

# Month

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__datetime.R#L261)

## Description

Extract month from underlying Date representation. Applies to Date and
Datetime columns. Returns the month number starting from 1. The return
value ranges from 1 to 12.

## Usage

<pre><code class='language-R'>ExprDT_month()
</code></pre>

## Value

Expr of month as UInt32

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
  pl$col("date")$dt$month()$alias("month")
)
```

    #> shape: (12, 2)
    #> ┌────────────┬───────┐
    #> │ date       ┆ month │
    #> │ ---        ┆ ---   │
    #> │ date       ┆ i8    │
    #> ╞════════════╪═══════╡
    #> │ 2020-12-25 ┆ 12    │
    #> │ 2020-12-26 ┆ 12    │
    #> │ 2020-12-27 ┆ 12    │
    #> │ 2020-12-28 ┆ 12    │
    #> │ …          ┆ …     │
    #> │ 2021-01-02 ┆ 1     │
    #> │ 2021-01-03 ┆ 1     │
    #> │ 2021-01-04 ┆ 1     │
    #> │ 2021-01-05 ┆ 1     │
    #> └────────────┴───────┘
