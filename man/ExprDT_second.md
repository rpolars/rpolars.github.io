

# Extract seconds from underlying Datetime representation

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__datetime.R#L442)

## Description

Applies to Datetime columns. Returns the integer second number from 0 to
59, or a floating point number from 0 \< 60 if
<code>fractional=TRUE</code> that includes any milli/micro/nanosecond
component.

## Usage

<pre><code class='language-R'>ExprDT_second(fractional = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_second_:_fractional">fractional</code>
</td>
<td>
A logical. Whether to include the fractional component of the second.
</td>
</tr>
</table>

## Value

Expr of data type Int8 or Float64

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
  second = pl$col("datetime")$dt$second(),
  second_fractional = pl$col("datetime")$dt$second(fractional = TRUE)
)
```

    #> shape: (3, 3)
    #> ┌─────────────────────────────┬────────┬───────────────────┐
    #> │ datetime                    ┆ second ┆ second_fractional │
    #> │ ---                         ┆ ---    ┆ ---               │
    #> │ datetime[ms, UTC]           ┆ i8     ┆ f64               │
    #> ╞═════════════════════════════╪════════╪═══════════════════╡
    #> │ 1978-01-01 01:01:01 UTC     ┆ 1      ┆ 1.0               │
    #> │ 2024-10-13 05:30:14.500 UTC ┆ 14     ┆ 14.5              │
    #> │ 2065-01-01 10:20:30.060 UTC ┆ 30     ┆ 30.06             │
    #> └─────────────────────────────┴────────┴───────────────────┘
