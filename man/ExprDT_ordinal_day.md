

# Ordinal Day

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__datetime.R#L362)

## Description

Extract ordinal day from underlying Date representation. Applies to Date
and Datetime columns. Returns the day of year starting from 1. The
return value ranges from 1 to 366. (The last day of year differs by
years.)

## Usage

<pre><code class='language-R'>ExprDT_ordinal_day()
</code></pre>

## Value

Expr of ordinal_day as UInt32

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
  pl$col("date")$dt$ordinal_day()$alias("ordinal_day")
)
```

    #> shape: (12, 2)
    #> ┌────────────┬─────────────┐
    #> │ date       ┆ ordinal_day │
    #> │ ---        ┆ ---         │
    #> │ date       ┆ i16         │
    #> ╞════════════╪═════════════╡
    #> │ 2020-12-25 ┆ 360         │
    #> │ 2020-12-26 ┆ 361         │
    #> │ 2020-12-27 ┆ 362         │
    #> │ 2020-12-28 ┆ 363         │
    #> │ 2020-12-29 ┆ 364         │
    #> │ …          ┆ …           │
    #> │ 2021-01-01 ┆ 1           │
    #> │ 2021-01-02 ┆ 2           │
    #> │ 2021-01-03 ┆ 3           │
    #> │ 2021-01-04 ┆ 4           │
    #> │ 2021-01-05 ┆ 5           │
    #> └────────────┴─────────────┘
