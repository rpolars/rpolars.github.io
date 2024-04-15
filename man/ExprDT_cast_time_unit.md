

# cast_time_unit

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__datetime.R#L635)

## Description

Cast the underlying data to another time unit. This may lose precision.
The corresponding global timepoint will stay unchanged +/- precision.

## Usage

<pre><code class='language-R'>ExprDT_cast_time_unit(tu = c("ns", "us", "ms"))
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_cast_time_unit_:_tu">tu</code>
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
    interval = "1d1s"
  )
)
df$select(
  pl$col("date"),
  pl$col("date")$dt$cast_time_unit()$alias("cast_time_unit_ns"),
  pl$col("date")$dt$cast_time_unit(tu = "ms")$alias("cast_time_unit_ms")
)
```

    #> shape: (2, 3)
    #> ┌─────────────────────┬─────────────────────┬─────────────────────┐
    #> │ date                ┆ cast_time_unit_ns   ┆ cast_time_unit_ms   │
    #> │ ---                 ┆ ---                 ┆ ---                 │
    #> │ datetime[μs]        ┆ datetime[ns]        ┆ datetime[ms]        │
    #> ╞═════════════════════╪═════════════════════╪═════════════════════╡
    #> │ 2001-01-01 00:00:00 ┆ 2001-01-01 00:00:00 ┆ 2001-01-01 00:00:00 │
    #> │ 2001-01-02 00:00:01 ┆ 2001-01-02 00:00:01 ┆ 2001-01-02 00:00:01 │
    #> └─────────────────────┴─────────────────────┴─────────────────────┘
