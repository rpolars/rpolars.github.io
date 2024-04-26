

# Convert a Unix timestamp to date(time)

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L1074)

## Description

Depending on the <code>time_unit</code> provided, this function will
return a different dtype:

<ul>
<li>

<code>time_unit = “d”</code> returns <code>pl$Date</code>

</li>
<li>

<code>time_unit = “s”</code> returns <code>pl$Datetime("us")</code>
(<code>pl$Datetime</code>’s default)

</li>
<li>

<code>time_unit = “ms”</code> returns <code>pl$Datetime("ms")</code>

</li>
<li>

<code>time_unit = “us”</code> returns <code>pl$Datetime("us")</code>

</li>
<li>

<code>time_unit = “ns”</code> returns <code>pl$Datetime("ns")</code>

</li>
</ul>

## Usage

<pre><code class='language-R'>pl_from_epoch(column, time_unit = "s")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="column">column</code>
</td>
<td>
An Expr from which integers will be parsed. If this is a float column,
then the decimal part of the float will be ignored. Character are parsed
as column names, but other literal values must be passed to
<code>pl$lit()</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="time_unit">time_unit</code>
</td>
<td>
One of <code>“ns”</code>, <code>“us”</code>, <code>“ms”</code>,
<code>“s”</code>, <code>“d”</code>
</td>
</tr>
</table>

## Value

Expr as Date or Datetime depending on the <code>time_unit</code>.

## Examples

``` r
library(polars)

# pass an integer column
df = pl$DataFrame(timestamp = c(1666683077, 1666683099))
df$with_columns(
  timestamp_to_datetime = pl$from_epoch(pl$col("timestamp"), time_unit = "s")
)
```

    #> shape: (2, 2)
    #> ┌───────────┬───────────────────────┐
    #> │ timestamp ┆ timestamp_to_datetime │
    #> │ ---       ┆ ---                   │
    #> │ f64       ┆ datetime[μs]          │
    #> ╞═══════════╪═══════════════════════╡
    #> │ 1.6667e9  ┆ 2022-10-25 07:31:17   │
    #> │ 1.6667e9  ┆ 2022-10-25 07:31:39   │
    #> └───────────┴───────────────────────┘

``` r
# pass a literal
pl$from_epoch(pl$lit(c(1666683077, 1666683099)), time_unit = "s")$to_series()
```

    #> polars Series: shape: (2,)
    #> Series: '' [datetime[μs]]
    #> [
    #>  2022-10-25 07:31:17
    #>  2022-10-25 07:31:39
    #> ]

``` r
# use different time_unit
df = pl$DataFrame(timestamp = c(12345, 12346))
df$with_columns(
  timestamp_to_date = pl$from_epoch(pl$col("timestamp"), time_unit = "d")
)
```

    #> shape: (2, 2)
    #> ┌───────────┬───────────────────┐
    #> │ timestamp ┆ timestamp_to_date │
    #> │ ---       ┆ ---               │
    #> │ f64       ┆ date              │
    #> ╞═══════════╪═══════════════════╡
    #> │ 12345.0   ┆ 2003-10-20        │
    #> │ 12346.0   ┆ 2003-10-21        │
    #> └───────────┴───────────────────┘
