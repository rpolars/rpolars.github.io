
# Convert a String column into a Datetime column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L171)

## Description

Convert a String column into a Datetime column

## Usage

<pre><code class='language-R'>ExprStr_to_datetime(
  format = NULL,
  time_unit = NULL,
  time_zone = NULL,
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
<code id="ExprStr_to_datetime_:_format">format</code>
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
<code id="ExprStr_to_datetime_:_time_unit">time_unit</code>
</td>
<td>
String (<code>“ns”</code>, <code>“us”</code>, <code>“ms”</code>) or
integer.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_time_zone">time_zone</code>
</td>
<td>
String describing a timezone. If <code>NULL</code> (default),
<code style="white-space: pre;">“GMT</code> is used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if a single string cannot
be parsed. If <code>FALSE</code>, parsing failure will produce a polars
<code>null</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_exact">exact</code>
</td>
<td>
If <code>TRUE</code> (default), require an exact format match.
Otherwise, allow the format to match anywhere in the target string.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_cache">cache</code>
</td>
<td>
Use a cache of unique, converted dates to apply the datetime conversion.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_ambiguous">ambiguous</code>
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

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(str_date = c("2009-01-02 01:00", "2009-01-03 02:00", "2009-1-4 3:00"))$
  with_columns(datetime = pl$col("str_date")$str$to_datetime(strict = FALSE))
```

    #> shape: (3, 2)
    #> ┌──────────────────┬─────────────────────┐
    #> │ str_date         ┆ datetime            │
    #> │ ---              ┆ ---                 │
    #> │ str              ┆ datetime[μs]        │
    #> ╞══════════════════╪═════════════════════╡
    #> │ 2009-01-02 01:00 ┆ 2009-01-02 01:00:00 │
    #> │ 2009-01-03 02:00 ┆ 2009-01-03 02:00:00 │
    #> │ 2009-1-4 3:00    ┆ 2009-01-04 03:00:00 │
    #> └──────────────────┴─────────────────────┘
