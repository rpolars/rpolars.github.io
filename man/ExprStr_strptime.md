

# Convert a String column into a Date/Datetime/Time column.

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__string.R#L61)

## Description

Convert a String column into a Date/Datetime/Time column.

## Usage

<pre><code class='language-R'>ExprStr_strptime(
  datatype,
  format,
  strict = TRUE,
  exact = TRUE,
  cache = TRUE,
  ambiguous = "raise"
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strptime_:_datatype">datatype</code>
</td>
<td>
The data type to convert into. Can be either Date, Datetime, or Time.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strptime_:_format">format</code>
</td>
<td>
Format to use for conversion. See <code>?strptime</code> for possible
values. Example: "%Y-%m-%d %H:%M:%S". If <code>NULL</code> (default),
the format is inferred from the data. Notice that time zone
<code style="white-space: pre;">%Z</code> is not supported and will just
ignore timezones. Numeric time zones like
<code style="white-space: pre;">%z</code> or
<code style="white-space: pre;">%:z</code> are supported.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strptime_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if a single string cannot
be parsed. Otherwise, produce a polars <code>null</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strptime_:_exact">exact</code>
</td>
<td>
If <code>TRUE</code> (default), require an exact format match.
Otherwise, allow the format to match anywhere in the target string.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strptime_:_cache">cache</code>
</td>
<td>
Use a cache of unique, converted dates to apply the datetime conversion.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strptime_:_ambiguous">ambiguous</code>
</td>
<td>

Determine how to deal with ambiguous datetimes:

<ul>
<li>

<code>“raise”</code> (default): raise

</li>
<li>

<code>“earliest”</code>: use the earliest datetime

</li>
<li>

<code>“latest”</code>: use the latest datetime

</li>
</ul>
</td>
</tr>
</table>

## Details

When parsing a Datetime the column precision will be inferred from the
format string, if given, eg: “%F %T%.3f” =\> Datetime("ms"). If no
fractional second component is found then the default is "us"
(microsecond).

## Value

Expr of a Date, Datetime or Time Series

## Examples

``` r
library(polars)

s = pl$Series(
  c(
    "2021-04-22",
    "2022-01-04 00:00:00",
    "01/31/22",
    "Sun Jul  8 00:34:60 2001"
  ),
  "date"
)
#' #join multiple passes with different format
s$to_frame()$with_columns(
  pl$col("date")
  $str$strptime(pl$Date, "%F", strict = FALSE)
  $fill_null(pl$col("date")$str$strptime(pl$Date, "%F %T", strict = FALSE))
  $fill_null(pl$col("date")$str$strptime(pl$Date, "%D", strict = FALSE))
  $fill_null(pl$col("date")$str$strptime(pl$Date, "%c", strict = FALSE))
)
```

    #> shape: (4, 1)
    #> ┌────────────┐
    #> │ date       │
    #> │ ---        │
    #> │ date       │
    #> ╞════════════╡
    #> │ 2021-04-22 │
    #> │ 2022-01-04 │
    #> │ 2022-01-31 │
    #> │ 2001-07-08 │
    #> └────────────┘

``` r
txt_datetimes = c(
  "2023-01-01 11:22:33 -0100",
  "2023-01-01 11:22:33 +0300",
  "invalid time"
)

pl$lit(txt_datetimes)$str$strptime(
  pl$Datetime("ns"),
  format = "%Y-%m-%d %H:%M:%S %z", strict = FALSE,
)$to_series()
```

    #> polars Series: shape: (3,)
    #> Series: '' [datetime[ns, UTC]]
    #> [
    #>  2023-01-01 12:22:33 UTC
    #>  2023-01-01 08:22:33 UTC
    #>  null
    #> ]
