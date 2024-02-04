

# timestamp

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__datetime.R#L594)

## Description

Return a timestamp in the given time unit.

## Usage

<pre><code class='language-R'>ExprDT_timestamp(tu = c("ns", "us", "ms"))
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_timestamp_:_tu">tu</code>
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
  pl$col("date")$dt$timestamp()$alias("timestamp_ns"),
  pl$col("date")$dt$timestamp(tu = "ms")$alias("timestamp_ms")
)
```

    #> shape: (2, 3)
    #> ┌─────────────────────┬────────────────────┬──────────────┐
    #> │ date                ┆ timestamp_ns       ┆ timestamp_ms │
    #> │ ---                 ┆ ---                ┆ ---          │
    #> │ datetime[μs]        ┆ i64                ┆ i64          │
    #> ╞═════════════════════╪════════════════════╪══════════════╡
    #> │ 2001-01-01 00:00:00 ┆ 978307200000000000 ┆ 978307200000 │
    #> │ 2001-01-02 00:00:01 ┆ 978393601000000000 ┆ 978393601000 │
    #> └─────────────────────┴────────────────────┴──────────────┘
