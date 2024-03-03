

# Microsecond

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__datetime.R#L491)

## Description

Extract microseconds from underlying Datetime representation. Applies to
Datetime columns.

## Usage

<pre><code class='language-R'>ExprDT_microsecond()
</code></pre>

## Value

Expr of microsecond as Int64

## Examples

``` r
library(polars)

pl$DataFrame(
  date = pl$date_range(
    as.numeric(as.POSIXct("2001-1-1")) * 1E6 + 456789, # manually convert to us
    as.numeric(as.POSIXct("2001-1-1 00:00:6")) * 1E6,
    interval = "2s654321us",
    time_unit = "us" # instruct polars input is us, and store as us
  )
)$with_columns(
  pl$col("date")$cast(pl$Int64)$alias("datetime int64"),
  pl$col("date")$dt$microsecond()$alias("microsecond")
)
```

    #> shape: (2_089, 3)
    #> ┌──────────────────────────────┬────────────────────┬─────────────┐
    #> │ date                         ┆ datetime int64     ┆ microsecond │
    #> │ ---                          ┆ ---                ┆ ---         │
    #> │ datetime[μs]                 ┆ i64                ┆ i32         │
    #> ╞══════════════════════════════╪════════════════════╪═════════════╡
    #> │ +32971-04-28 00:07:36.789    ┆ 978307200456789000 ┆ 789000      │
    #> │ +32971-04-28 00:07:39.443321 ┆ 978307200459443321 ┆ 443321      │
    #> │ +32971-04-28 00:07:42.097642 ┆ 978307200462097642 ┆ 97642       │
    #> │ +32971-04-28 00:07:44.751963 ┆ 978307200464751963 ┆ 751963      │
    #> │ +32971-04-28 00:07:47.406284 ┆ 978307200467406284 ┆ 406284      │
    #> │ …                            ┆ …                  ┆ …           │
    #> │ +32971-04-28 01:39:48.393964 ┆ 978307205988393964 ┆ 393964      │
    #> │ +32971-04-28 01:39:51.048285 ┆ 978307205991048285 ┆ 48285       │
    #> │ +32971-04-28 01:39:53.702606 ┆ 978307205993702606 ┆ 702606      │
    #> │ +32971-04-28 01:39:56.356927 ┆ 978307205996356927 ┆ 356927      │
    #> │ +32971-04-28 01:39:59.011248 ┆ 978307205999011248 ┆ 11248       │
    #> └──────────────────────────────┴────────────────────┴─────────────┘
