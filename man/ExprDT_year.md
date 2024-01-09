
# Year

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__datetime.R#L177)

## Description

Extract year from underlying Date representation. Applies to Date and
Datetime columns. Returns the year number in the calendar date.

## Usage

<pre><code class='language-R'>ExprDT_year()
</code></pre>

## Value

Expr of Year as Int32

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
  pl$col("date")$dt$year()$alias("year"),
  pl$col("date")$dt$iso_year()$alias("iso_year")
)
```

    #> shape: (12, 3)
    #> ┌────────────┬──────┬──────────┐
    #> │ date       ┆ year ┆ iso_year │
    #> │ ---        ┆ ---  ┆ ---      │
    #> │ date       ┆ i32  ┆ i32      │
    #> ╞════════════╪══════╪══════════╡
    #> │ 2020-12-25 ┆ 2020 ┆ 2020     │
    #> │ 2020-12-26 ┆ 2020 ┆ 2020     │
    #> │ 2020-12-27 ┆ 2020 ┆ 2020     │
    #> │ 2020-12-28 ┆ 2020 ┆ 2020     │
    #> │ …          ┆ …    ┆ …        │
    #> │ 2021-01-02 ┆ 2021 ┆ 2020     │
    #> │ 2021-01-03 ┆ 2021 ┆ 2020     │
    #> │ 2021-01-04 ┆ 2021 ┆ 2021     │
    #> │ 2021-01-05 ┆ 2021 ┆ 2021     │
    #> └────────────┴──────┴──────────┘
