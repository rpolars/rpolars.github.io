

# Nanosecond

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__datetime.R#L532)

## Description

Extract seconds from underlying Datetime representation. Applies to
Datetime columns. Returns the integer second number from 0 to 59, or a
floating point number from 0 \< 60 if <code>fractional=True</code> that
includes any milli/micro/nanosecond component.

## Usage

<pre><code class='language-R'>ExprDT_nanosecond()
</code></pre>

## Value

Expr of second as Int64

## Examples

``` r
library(polars)

pl$DataFrame(date = pl$date_range(
  as.numeric(as.POSIXct("2001-1-1")) * 1E9 + 123456789, # manually convert to us
  as.numeric(as.POSIXct("2001-1-1 00:00:6")) * 1E9,
  interval = "1s987654321ns",
  time_unit = "ns", # instruct polars input is us, and store as us
  eager = TRUE
))$with_columns(
  pl$col("date")$cast(pl$Int64)$alias("datetime int64"),
  pl$col("date")$dt$nanosecond()$alias("nanosecond")
)
```

    #> shape: (2_956_522, 3)
    #> ┌───────────────────────────────┬─────────────────────┬────────────┐
    #> │ date                          ┆ datetime int64      ┆ nanosecond │
    #> │ ---                           ┆ ---                 ┆ ---        │
    #> │ datetime[ns]                  ┆ i64                 ┆ i32        │
    #> ╞═══════════════════════════════╪═════════════════════╪════════════╡
    #> │ 2051-08-06 07:05:44.407597056 ┆ 2574918344407597056 ┆ 407597056  │
    #> │ 2051-08-06 07:05:46.395251377 ┆ 2574918346395251377 ┆ 395251377  │
    #> │ 2051-08-06 07:05:48.382905698 ┆ 2574918348382905698 ┆ 382905698  │
    #> │ 2051-08-06 07:05:50.370560019 ┆ 2574918350370560019 ┆ 370560019  │
    #> │ …                             ┆ …                   ┆ …          │
    #> │ 2051-10-13 07:28:00.185411334 ┆ 2580794880185411334 ┆ 185411334  │
    #> │ 2051-10-13 07:28:02.173065655 ┆ 2580794882173065655 ┆ 173065655  │
    #> │ 2051-10-13 07:28:04.160719976 ┆ 2580794884160719976 ┆ 160719976  │
    #> │ 2051-10-13 07:28:06.148374297 ┆ 2580794886148374297 ┆ 148374297  │
    #> └───────────────────────────────┴─────────────────────┴────────────┘
