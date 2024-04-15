

# Hour

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__datetime.R#L388)

## Description

Extract hour from underlying Datetime representation. Applies to
Datetime columns. Returns the hour number from 0 to 23.

## Usage

<pre><code class='language-R'>ExprDT_hour()
</code></pre>

## Value

Expr of hour as UInt32

## Examples

``` r
library(polars)

df = pl$DataFrame(
  date = pl$date_range(
    as.Date("2020-12-25"),
    as.Date("2021-1-05"),
    interval = "1d2h",
    time_zone = "GMT"
  )
)
df$with_columns(
  pl$col("date")$dt$hour()$alias("hour")
)
```

    #> shape: (11, 2)
    #> ┌─────────────────────────┬──────┐
    #> │ date                    ┆ hour │
    #> │ ---                     ┆ ---  │
    #> │ datetime[μs, GMT]       ┆ i8   │
    #> ╞═════════════════════════╪══════╡
    #> │ 2020-12-25 00:00:00 GMT ┆ 0    │
    #> │ 2020-12-26 02:00:00 GMT ┆ 2    │
    #> │ 2020-12-27 04:00:00 GMT ┆ 4    │
    #> │ 2020-12-28 06:00:00 GMT ┆ 6    │
    #> │ 2020-12-29 08:00:00 GMT ┆ 8    │
    #> │ …                       ┆ …    │
    #> │ 2020-12-31 12:00:00 GMT ┆ 12   │
    #> │ 2021-01-01 14:00:00 GMT ┆ 14   │
    #> │ 2021-01-02 16:00:00 GMT ┆ 16   │
    #> │ 2021-01-03 18:00:00 GMT ┆ 18   │
    #> │ 2021-01-04 20:00:00 GMT ┆ 20   │
    #> └─────────────────────────┴──────┘
