
# Days

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__datetime.R#L754)

## Description

Extract the days from a Duration type.

## Usage

<pre><code class='language-R'>ExprDT_total_days()
</code></pre>

## Value

Expr of i64

## Examples

``` r
library(polars)

df = pl$DataFrame(
  date = pl$date_range(
    start = as.Date("2020-3-1"),
    end = as.Date("2020-5-1"),
    interval = "1mo",
    eager = TRUE
  )
)
df$select(
  pl$col("date"),
  diff_days = pl$col("date")$diff()$dt$total_days()
)
```

    #> shape: (3, 2)
    #> ┌────────────┬───────────┐
    #> │ date       ┆ diff_days │
    #> │ ---        ┆ ---       │
    #> │ date       ┆ i64       │
    #> ╞════════════╪═══════════╡
    #> │ 2020-03-01 ┆ null      │
    #> │ 2020-04-01 ┆ 31        │
    #> │ 2020-05-01 ┆ 30        │
    #> └────────────┴───────────┘
