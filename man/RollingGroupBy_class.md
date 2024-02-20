

# Operations on Polars DataFrame grouped by rolling windows

## Description

This class comes from <code>\<DataFrame\>$rolling()</code>.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  dt = c("2020-01-01", "2020-01-01", "2020-01-01", "2020-01-02", "2020-01-03", "2020-01-08"),
  a = c(3, 7, 5, 9, 2, 1)
)$with_columns(
  pl$col("dt")$str$strptime(pl$Date, format = NULL)$set_sorted()
)

df$rolling(index_column = "dt", period = "2d")
```

    #> shape: (6, 2)
    #> ┌────────────┬─────┐
    #> │ dt         ┆ a   │
    #> │ ---        ┆ --- │
    #> │ date       ┆ f64 │
    #> ╞════════════╪═════╡
    #> │ 2020-01-01 ┆ 3.0 │
    #> │ 2020-01-01 ┆ 7.0 │
    #> │ 2020-01-01 ┆ 5.0 │
    #> │ 2020-01-02 ┆ 9.0 │
    #> │ 2020-01-03 ┆ 2.0 │
    #> │ 2020-01-08 ┆ 1.0 │
    #> └────────────┴─────┘
