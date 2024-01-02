
# Minutes

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__datetime.R#L844)

## Description

Extract the minutes from a Duration type.

## Usage

<pre><code class='language-R'>ExprDT_total_minutes()
</code></pre>

## Value

Expr of i64

## Examples

``` r
library(polars)

df = pl$DataFrame(
  date = pl$date_range(
    start = as.Date("2020-1-1"),
    end = as.Date("2020-1-4"),
    interval = "1d",
    eager = TRUE
  )
)
df$select(
  pl$col("date"),
  diff_minutes = pl$col("date")$diff()$dt$total_minutes()
)
```

    #> shape: (4, 2)
    #> ┌────────────┬──────────────┐
    #> │ date       ┆ diff_minutes │
    #> │ ---        ┆ ---          │
    #> │ date       ┆ i64          │
    #> ╞════════════╪══════════════╡
    #> │ 2020-01-01 ┆ null         │
    #> │ 2020-01-02 ┆ 1440         │
    #> │ 2020-01-03 ┆ 1440         │
    #> │ 2020-01-04 ┆ 1440         │
    #> └────────────┴──────────────┘
