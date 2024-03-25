

# Convert a String column into a Date/Datetime/Time column.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L84)

## Description

Similar to the <code>strptime()</code> function.

## Usage

<pre><code class='language-R'>ExprStr_strptime(
  dtype,
  format = NULL,
  ...,
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
<code id="ExprStr_strptime_:_dtype">dtype</code>
</td>
<td>
The data type to convert into. Can be either <code>pl$Date</code>,
<code>pl$Datetime()</code>, or <code>pl$Time</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strptime_:_format">format</code>
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
<code id="ExprStr_strptime_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strptime_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if a single string cannot
be parsed. If <code>FALSE</code>, produce a polars <code>null</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strptime_:_exact">exact</code>
</td>
<td>
If <code>TRUE</code> (default), require an exact format match. If
<code>FALSE</code>, allow the format to match anywhere in the target
string. Conversion to the Time type is always exact. Note that using
<code>exact = FALSE</code> introduces a performance penalty - cleaning
your data beforehand will almost certainly be more performant.
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

## Details

When parsing a Datetime the column precision will be inferred from the
format string, if given, e.g.: <code>“%F %T%.3f”</code> =\>
<code>pl$Datetime("ms")</code>. If no fractional second component is
found then the default is <code>“us”</code> (microsecond).

## Value

Expr of Date, Datetime or Time type

## See Also

<ul>
<li>

<code>\<Expr\>$str$to_date()</code>

</li>
<li>

<code>\<Expr\>$str$to_datetime()</code>

</li>
<li>

<code>\<Expr\>$str$to_time()</code>

</li>
</ul>

## Examples

``` r
library(polars)

# Dealing with a consistent format
s = pl$Series(c("2020-01-01 01:00Z", "2020-01-01 02:00Z"))

s$str$strptime(pl$Datetime(), "%Y-%m-%d %H:%M%#z")
```

    #> polars Series: shape: (2,)
    #> Series: '' [datetime[μs, UTC]]
    #> [
    #>  2020-01-01 01:00:00 UTC
    #>  2020-01-01 02:00:00 UTC
    #> ]

``` r
# Auto infer format
s$str$strptime(pl$Datetime())
```

    #> polars Series: shape: (2,)
    #> Series: '' [datetime[μs, UTC]]
    #> [
    #>  2020-01-01 01:00:00 UTC
    #>  2020-01-01 02:00:00 UTC
    #> ]

``` r
# Datetime with timezone is interpreted as UTC timezone
pl$Series("2020-01-01T01:00:00+09:00")$str$strptime(pl$Datetime())
```

    #> polars Series: shape: (1,)
    #> Series: '' [datetime[μs, UTC]]
    #> [
    #>  2019-12-31 16:00:00 UTC
    #> ]

``` r
# Dealing with different formats.
s = pl$Series(
  c(
    "2021-04-22",
    "2022-01-04 00:00:00",
    "01/31/22",
    "Sun Jul  8 00:34:60 2001"
  ),
  "date"
)

s$to_frame()$select(
  pl$coalesce(
    pl$col("date")$str$strptime(pl$Date, "%F", strict = FALSE),
    pl$col("date")$str$strptime(pl$Date, "%F %T", strict = FALSE),
    pl$col("date")$str$strptime(pl$Date, "%D", strict = FALSE),
    pl$col("date")$str$strptime(pl$Date, "%c", strict = FALSE)
  )
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
# Ignore invalid time
s = pl$Series(
  c(
    "2023-01-01 11:22:33 -0100",
    "2023-01-01 11:22:33 +0300",
    "invalid time"
  )
)

s$str$strptime(
  pl$Datetime("ns"),
  format = "%Y-%m-%d %H:%M:%S %z",
  strict = FALSE
)
```

    #> polars Series: shape: (3,)
    #> Series: '' [datetime[ns, UTC]]
    #> [
    #>  2023-01-01 12:22:33 UTC
    #>  2023-01-01 08:22:33 UTC
    #>  null
    #> ]
