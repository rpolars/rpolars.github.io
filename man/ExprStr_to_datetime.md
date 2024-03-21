

# Convert a String column into a Datetime column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L181)

## Description

Convert a String column into a Datetime column

## Usage

<pre><code class='language-R'>ExprStr_to_datetime(
  format = NULL,
  ...,
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
Format to use for conversion. Refer to
<a href="https://docs.rs/chrono/latest/chrono/format/strftime/index.html">the
chrono crate documentation</a> for the full specification. Example:
<code>“%Y-%m-%d %H:%M:%S”</code>. If <code>NULL</code> (default), the
format is inferred from the data. Notice that time zone
<code style="white-space: pre;">%Z</code> is not supported and will just
ignore timezones. Numeric time zones like
<code style="white-space: pre;">%z</code> or
<code style="white-space: pre;">%:z</code> are supported.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_time_unit">time_unit</code>
</td>
<td>
Unit of time for the resulting Datetime column. If <code>NULL</code>
(default), the time unit is inferred from the format string if given,
e.g.: <code>“%F %T%.3f”</code> =\> <code>pl$Datetime("ms")</code>. If no
fractional second component is found, the default is <code>“us”</code>
(microsecond).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_time_zone">time_zone</code>
</td>
<td>
for the resulting Datetime column.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if a single string cannot
be parsed. If <code>FALSE</code>, produce a polars <code>null</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_datetime_:_exact">exact</code>
</td>
<td>
If <code>TRUE</code> (default), require an exact format match. If
<code>FALSE</code>, allow the format to match anywhere in the target
string. Note that using <code>exact = FALSE</code> introduces a
performance penalty - cleaning your data beforehand will almost
certainly be more performant.
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

<code>“raise”</code> (default): throw an error

</li>
<li>

<code>“earliest”</code>: use the earliest datetime

</li>
<li>

<code>“latest”</code>: use the latest datetime

</li>
<li>

<code>“null”</code>: return a null value

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr of Datetime type

## See Also

<ul>
<li>

<code>\<Expr\>$str$strptime()</code>

</li>
</ul>

## Examples

``` r
library(polars)

s = pl$Series(c("2020-01-01 01:00Z", "2020-01-01 02:00Z"))

s$str$to_datetime("%Y-%m-%d %H:%M%#z")
```

    #> polars Series: shape: (2,)
    #> Series: '' [datetime[μs, UTC]]
    #> [
    #>  2020-01-01 01:00:00 UTC
    #>  2020-01-01 02:00:00 UTC
    #> ]

``` r
s$str$to_datetime(time_unit = "ms")
```

    #> polars Series: shape: (2,)
    #> Series: '' [datetime[ms, UTC]]
    #> [
    #>  2020-01-01 01:00:00 UTC
    #>  2020-01-01 02:00:00 UTC
    #> ]
