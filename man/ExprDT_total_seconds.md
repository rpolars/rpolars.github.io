

# Seconds

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__datetime.R#L809)

## Description

Extract the seconds from a Duration type.

## Usage

<pre><code class='language-R'>ExprDT_total_seconds()
</code></pre>

## Value

Expr of i64

## Examples

``` r
library(polars)

df = pl$DataFrame(date = pl$date_range(
  start = as.POSIXct("2020-1-1", tz = "GMT"),
  end = as.POSIXct("2020-1-1 00:04:00", tz = "GMT"),
  interval = "1m"
))
df$select(
  pl$col("date"),
  diff_sec = pl$col("date")$diff()$dt$total_seconds()
)
```

    #> shape: (5, 2)
    #> ┌─────────────────────────┬──────────┐
    #> │ date                    ┆ diff_sec │
    #> │ ---                     ┆ ---      │
    #> │ datetime[ms, GMT]       ┆ i64      │
    #> ╞═════════════════════════╪══════════╡
    #> │ 2020-01-01 00:00:00 GMT ┆ null     │
    #> │ 2020-01-01 00:01:00 GMT ┆ 60       │
    #> │ 2020-01-01 00:02:00 GMT ┆ 60       │
    #> │ 2020-01-01 00:03:00 GMT ┆ 60       │
    #> │ 2020-01-01 00:04:00 GMT ┆ 60       │
    #> └─────────────────────────┴──────────┘
