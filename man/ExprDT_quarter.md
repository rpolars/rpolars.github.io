

# Quarter

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__datetime.R#L234)

## Description

Extract quarter from underlying Date representation. Applies to Date and
Datetime columns. Returns the quarter ranging from 1 to 4.

## Usage

<pre><code class='language-R'>ExprDT_quarter()
</code></pre>

## Value

Expr of quarter as UInt32

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
  pl$col("date")$dt$quarter()$alias("quarter")
)
```

    #> shape: (12, 2)
    #> ┌────────────┬─────────┐
    #> │ date       ┆ quarter │
    #> │ ---        ┆ ---     │
    #> │ date       ┆ i8      │
    #> ╞════════════╪═════════╡
    #> │ 2020-12-25 ┆ 4       │
    #> │ 2020-12-26 ┆ 4       │
    #> │ 2020-12-27 ┆ 4       │
    #> │ 2020-12-28 ┆ 4       │
    #> │ 2020-12-29 ┆ 4       │
    #> │ …          ┆ …       │
    #> │ 2021-01-01 ┆ 1       │
    #> │ 2021-01-02 ┆ 1       │
    #> │ 2021-01-03 ┆ 1       │
    #> │ 2021-01-04 ┆ 1       │
    #> │ 2021-01-05 ┆ 1       │
    #> └────────────┴─────────┘
