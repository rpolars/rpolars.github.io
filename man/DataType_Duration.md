

# Data type representing a time duration

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/datatype.R#L204)

## Description

Data type representing a time duration

## Usage

<pre><code class='language-R'>DataType_Duration(time_unit = "us")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Duration_:_time_unit">time_unit</code>
</td>
<td>
Unit of time. One of <code>“ms”</code>, <code>“us”</code> (default) or
<code>“ns”</code>.
</td>
</tr>
</table>

## Value

Duration DataType

## Examples

``` r
library(polars)

test = pl$DataFrame(
  a = 1:2,
  b = c("a", "b"),
  c = pl$duration(weeks = c(1, 2), days = c(0, 2))
)

# select all columns of type "duration"
test$select(pl$col(pl$Duration()))
```

    #> shape: (2, 1)
    #> ┌──────────────┐
    #> │ c            │
    #> │ ---          │
    #> │ duration[μs] │
    #> ╞══════════════╡
    #> │ 7d           │
    #> │ 16d          │
    #> └──────────────┘
