

# Extract milliseconds from underlying Datetime representation

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__datetime.R#L471)

## Description

Applies to Datetime columns.

## Usage

<pre><code class='language-R'>ExprDT_millisecond()
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
  millisecond = pl$col("datetime")$dt$millisecond()
)
```

    #> shape: (3, 2)
    #> ┌─────────────────────────────┬─────────────┐
    #> │ datetime                    ┆ millisecond │
    #> │ ---                         ┆ ---         │
    #> │ datetime[ms, UTC]           ┆ i32         │
    #> ╞═════════════════════════════╪═════════════╡
    #> │ 1978-01-01 01:01:01 UTC     ┆ 0           │
    #> │ 2024-10-13 05:30:14.500 UTC ┆ 500         │
    #> │ 2065-01-01 10:20:30.060 UTC ┆ 60          │
    #> └─────────────────────────────┴─────────────┘
