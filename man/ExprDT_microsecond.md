

# Extract microseconds from underlying Datetime representation.

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__datetime.R#L493)

## Description

Applies to Datetime columns.

## Usage

<pre><code class='language-R'>ExprDT_microsecond()
</code></pre>

## Value

Expr of data type Int32

## Examples

``` r
library(polars)

df = pl$DataFrame(
  datetime = as.POSIXct(
    c(
      "1978-01-01 01:01:01",
      "2024-10-13 05:30:14.500",
      "2065-01-01 10:20:30.06"
    ),
    "UTC"
  )
)

df$with_columns(
  microsecond = pl$col("datetime")$dt$microsecond()
)
```

    #> shape: (3, 2)
    #> ┌─────────────────────────────┬─────────────┐
    #> │ datetime                    ┆ microsecond │
    #> │ ---                         ┆ ---         │
    #> │ datetime[ms, UTC]           ┆ i32         │
    #> ╞═════════════════════════════╪═════════════╡
    #> │ 1978-01-01 01:01:01 UTC     ┆ 0           │
    #> │ 2024-10-13 05:30:14.500 UTC ┆ 500000      │
    #> │ 2065-01-01 10:20:30.060 UTC ┆ 60000       │
    #> └─────────────────────────────┴─────────────┘
