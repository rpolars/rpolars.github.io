

# Extract nanoseconds from underlying Datetime representation

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__datetime.R#L515)

## Description

Applies to Datetime columns.

## Usage

<pre><code class='language-R'>ExprDT_nanosecond()
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
  nanosecond = pl$col("datetime")$dt$nanosecond()
)
```

    #> shape: (3, 2)
    #> ┌─────────────────────────────┬────────────┐
    #> │ datetime                    ┆ nanosecond │
    #> │ ---                         ┆ ---        │
    #> │ datetime[ms, UTC]           ┆ i32        │
    #> ╞═════════════════════════════╪════════════╡
    #> │ 1978-01-01 01:01:01 UTC     ┆ 0          │
    #> │ 2024-10-13 05:30:14.500 UTC ┆ 500000000  │
    #> │ 2065-01-01 10:20:30.060 UTC ┆ 60000000   │
    #> └─────────────────────────────┴────────────┘
