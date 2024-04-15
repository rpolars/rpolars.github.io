

# Weekday

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__datetime.R#L309)

## Description

Extract the week day from the underlying Date representation. Applies to
Date and Datetime columns. Returns the ISO weekday number where monday =
1 and sunday = 7

## Usage

<pre><code class='language-R'>ExprDT_weekday()
</code></pre>

## Value

Expr of weekday as UInt32

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
  pl$col("date")$dt$weekday()$alias("weekday")
)
```

    #> shape: (12, 2)
    #> ┌────────────┬─────────┐
    #> │ date       ┆ weekday │
    #> │ ---        ┆ ---     │
    #> │ date       ┆ i8      │
    #> ╞════════════╪═════════╡
    #> │ 2020-12-25 ┆ 5       │
    #> │ 2020-12-26 ┆ 6       │
    #> │ 2020-12-27 ┆ 7       │
    #> │ 2020-12-28 ┆ 1       │
    #> │ 2020-12-29 ┆ 2       │
    #> │ …          ┆ …       │
    #> │ 2021-01-01 ┆ 5       │
    #> │ 2021-01-02 ┆ 6       │
    #> │ 2021-01-03 ┆ 7       │
    #> │ 2021-01-04 ┆ 1       │
    #> │ 2021-01-05 ┆ 2       │
    #> └────────────┴─────────┘
