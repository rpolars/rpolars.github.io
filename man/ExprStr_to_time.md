

# Convert a String column into a Time column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L157)

## Description

Convert a String column into a Time column

## Usage

<pre><code class='language-R'>ExprStr_to_time(format = NULL, ..., strict = TRUE, cache = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_time_:_format">format</code>
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
<code id="ExprStr_to_time_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_time_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if a single string cannot
be parsed. If <code>FALSE</code>, produce a polars <code>null</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_time_:_cache">cache</code>
</td>
<td>
Use a cache of unique, converted dates to apply the datetime conversion.
</td>
</tr>
</table>

## Format

Format to use for conversion. Refer to
<a href="https://docs.rs/chrono/latest/chrono/format/strftime/index.html">the
chrono crate documentation</a> for the full specification. Example:
<code>“%H:%M:%S”</code>. If <code>NULL</code> (default), the format is
inferred from the data.

## Value

Expr of Time type

## See Also

<ul>
<li>

<code>\<Expr\>$str$strptime()</code>

</li>
</ul>

## Examples

``` r
library(polars)

s = pl$Series(c("01:00", "02:00", "03:00"))

s$str$to_time("%H:%M")
```

    #> polars Series: shape: (3,)
    #> Series: '' [time]
    #> [
    #>  01:00:00
    #>  02:00:00
    #>  03:00:00
    #> ]
