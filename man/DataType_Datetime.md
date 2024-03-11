

# Data type representing a calendar date and time of day.

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/datatype.R#L186)

## Description

The underlying representation of this type is a 64-bit signed integer.
The integer indicates the number of time units since the Unix epoch
(1970-01-01 00:00:00). The number can be negative to indicate datetimes
before the epoch.

## Usage

<pre><code class='language-R'>DataType_Datetime(time_unit = "us", time_zone = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Datetime_:_time_unit">time_unit</code>
</td>
<td>
Unit of time. One of <code>“ms”</code>, <code>“us”</code> (default) or
<code>“ns”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Datetime_:_time_zone">time_zone</code>
</td>
<td>
Time zone string, as defined in <code>OlsonNames()</code>. Setting
<code>timezone = “\*“</code> will match any timezone, which can be
useful to select all Datetime columns containing a timezone.
</td>
</tr>
</table>

## Value

Datetime DataType

## Examples

``` r
library(polars)

pl$Datetime("ns", "Pacific/Samoa")
```

    #> DataType: Datetime(
    #>     Nanoseconds,
    #>     Some(
    #>         "Pacific/Samoa",
    #>     ),
    #> )

``` r
df = pl$DataFrame(
  naive_time = as.POSIXct("1900-01-01"),
  zoned_time = as.POSIXct("1900-01-01", "UTC")
)
df
```

    #> shape: (1, 2)
    #> ┌─────────────────────┬─────────────────────────┐
    #> │ naive_time          ┆ zoned_time              │
    #> │ ---                 ┆ ---                     │
    #> │ datetime[ms]        ┆ datetime[ms, UTC]       │
    #> ╞═════════════════════╪═════════════════════════╡
    #> │ 1900-01-01 00:00:00 ┆ 1900-01-01 00:00:00 UTC │
    #> └─────────────────────┴─────────────────────────┘

``` r
df$select(pl$col(pl$Datetime("us", "*")))
```

    #> shape: (0, 0)
    #> ┌┐
    #> ╞╡
    #> └┘
