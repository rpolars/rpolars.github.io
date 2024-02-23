

# with_time_unit

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__datetime.R#L624)

## Description

Set time unit of a Series of dtype Datetime or Duration. This does not
modify underlying data, and should be used to fix an incorrect time
unit. The corresponding global timepoint will change.

## Usage

<pre><code class='language-R'>ExprDT_with_time_unit(tu = c("ns", "us", "ms"))
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_with_time_unit_:_tu">tu</code>
</td>
<td>
string option either ‘ns’, ‘us’, or ‘ms’
</td>
</tr>
</table>

## Value

Expr of i64

## Examples

``` r
library(polars)

df = pl$DataFrame(
  date = pl$date_range(
    start = as.Date("2001-1-1"),
    end = as.Date("2001-1-3"),
    interval = "1d1s",
    eager = TRUE
  )
)
df$select(
  pl$col("date"),
  pl$col("date")$dt$with_time_unit()$alias("with_time_unit_ns"),
  pl$col("date")$dt$with_time_unit(tu = "ms")$alias("with_time_unit_ms")
)
```

    #> shape: (2, 3)
    #> ┌─────────────────────┬─────────────────────────┬───────────────────────┐
    #> │ date                ┆ with_time_unit_ns       ┆ with_time_unit_ms     │
    #> │ ---                 ┆ ---                     ┆ ---                   │
    #> │ datetime[μs]        ┆ datetime[ns]            ┆ datetime[ms]          │
    #> ╞═════════════════════╪═════════════════════════╪═══════════════════════╡
    #> │ 2001-01-01 00:00:00 ┆ 1970-01-12 07:45:07.200 ┆ +32971-04-28 00:00:00 │
    #> │ 2001-01-02 00:00:01 ┆ 1970-01-12 07:46:33.601 ┆ +32974-01-22 00:16:40 │
    #> └─────────────────────┴─────────────────────────┴───────────────────────┘
