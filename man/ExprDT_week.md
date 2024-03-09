

# Week

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/expr__datetime.R#L284)

## Description

Extract the week from the underlying Date representation. Applies to
Date and Datetime columns. Returns the ISO week number starting from 1.
The return value ranges from 1 to 53. (The last week of year differs by
years.)

## Usage

<pre><code class='language-R'>ExprDT_week()
</code></pre>

## Value

Expr of week as UInt32

## Examples

``` r
library(polars)

df = pl$DataFrame(
  date = pl$date_range(
    as.Date("2020-12-25"),
    as.Date("2021-1-05"),
    interval = "1d",
    time_zone = "GMT"
  )
)
df$with_columns(
  pl$col("date")$dt$week()$alias("week")
)
```

    #> shape: (12, 2)
    #> ┌────────────┬──────┐
    #> │ date       ┆ week │
    #> │ ---        ┆ ---  │
    #> │ date       ┆ i8   │
    #> ╞════════════╪══════╡
    #> │ 2020-12-25 ┆ 52   │
    #> │ 2020-12-26 ┆ 52   │
    #> │ 2020-12-27 ┆ 52   │
    #> │ 2020-12-28 ┆ 53   │
    #> │ 2020-12-29 ┆ 53   │
    #> │ …          ┆ …    │
    #> │ 2021-01-01 ┆ 53   │
    #> │ 2021-01-02 ┆ 53   │
    #> │ 2021-01-03 ┆ 53   │
    #> │ 2021-01-04 ┆ 1    │
    #> │ 2021-01-05 ┆ 1    │
    #> └────────────┴──────┘
