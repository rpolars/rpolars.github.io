

# Convert a String column into a Time column

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__string.R#L140)

## Description

Convert a String column into a Time column

## Usage

<pre><code class='language-R'>ExprStr_to_time(format = NULL, strict = TRUE, cache = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_time_:_format">format</code>
</td>
<td>
Format to use for conversion. See <code>?strptime</code> for possible
values. Example: "%H:%M:%S". If <code>NULL</code> (default), the format
is inferred from the data. Notice that time zone
<code style="white-space: pre;">%Z</code> is not supported and will just
ignore timezones. Numeric time zones like
<code style="white-space: pre;">%z</code> or
<code style="white-space: pre;">%:z</code> are supported.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_time_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if a single string cannot
be parsed. If <code>FALSE</code>, parsing failure will produce a polars
<code>null</code>.
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

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(str_time = c("01:20:01", "28:00:02", "03:00:02"))$
  with_columns(time = pl$col("str_time")$str$to_time(strict = FALSE))
```

    #> shape: (3, 2)
    #> ┌──────────┬──────────┐
    #> │ str_time ┆ time     │
    #> │ ---      ┆ ---      │
    #> │ str      ┆ time     │
    #> ╞══════════╪══════════╡
    #> │ 01:20:01 ┆ 01:20:01 │
    #> │ 28:00:02 ┆ null     │
    #> │ 03:00:02 ┆ 03:00:02 │
    #> └──────────┴──────────┘
