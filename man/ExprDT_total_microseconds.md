

# microseconds

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__datetime.R#L867)

## Description

Extract the microseconds from a Duration type.

## Usage

<pre><code class='language-R'>ExprDT_total_microseconds()
</code></pre>

## Value

Expr of i64

## Examples

``` r
library(polars)

df = pl$DataFrame(date = pl$date_range(
  start = as.POSIXct("2020-1-1", tz = "GMT"),
  end = as.POSIXct("2020-1-1 00:00:01", tz = "GMT"),
  interval = "1ms"
))
df$select(
  pl$col("date"),
  diff_microsec = pl$col("date")$diff()$dt$total_microseconds()
)
```

    #> shape: (1_001, 2)
    #> ┌─────────────────────────────┬───────────────┐
    #> │ date                        ┆ diff_microsec │
    #> │ ---                         ┆ ---           │
    #> │ datetime[μs, GMT]           ┆ i64           │
    #> ╞═════════════════════════════╪═══════════════╡
    #> │ 2020-01-01 00:00:00 GMT     ┆ null          │
    #> │ 2020-01-01 00:00:00.001 GMT ┆ 1000          │
    #> │ 2020-01-01 00:00:00.002 GMT ┆ 1000          │
    #> │ 2020-01-01 00:00:00.003 GMT ┆ 1000          │
    #> │ 2020-01-01 00:00:00.004 GMT ┆ 1000          │
    #> │ …                           ┆ …             │
    #> │ 2020-01-01 00:00:00.996 GMT ┆ 1000          │
    #> │ 2020-01-01 00:00:00.997 GMT ┆ 1000          │
    #> │ 2020-01-01 00:00:00.998 GMT ┆ 1000          │
    #> │ 2020-01-01 00:00:00.999 GMT ┆ 1000          │
    #> │ 2020-01-01 00:00:01 GMT     ┆ 1000          │
    #> └─────────────────────────────┴───────────────┘
