
# Convert a Utf8 column into a Date column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L118)

## Description

Convert a Utf8 column into a Date column

## Usage

<pre><code class='language-R'>ExprStr_to_date(format = NULL, strict = TRUE, exact = TRUE, cache = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_date_:_format">format</code>
</td>
<td>
Format to use for conversion. See <code>?strptime</code> for possible
values. Example: "%Y-%m-%d". If <code>NULL</code> (default), the format
is inferred from the data. Notice that time zone
<code style="white-space: pre;">%Z</code> is not supported and will just
ignore timezones. Numeric time zones like
<code style="white-space: pre;">%z</code> or
<code style="white-space: pre;">%:z</code> are supported.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_date_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if a single string cannot
be parsed. If <code>FALSE</code>, parsing failure will produce a polars
<code>null</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_date_:_exact">exact</code>
</td>
<td>
If <code>TRUE</code> (default), require an exact format match.
Otherwise, allow the format to match anywhere in the target string.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_date_:_cache">cache</code>
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

pl$DataFrame(str_date = c("2009-01-02", "2009-01-03", "2009-1-4", "2009 05 01"))$
  with_columns(date = pl$col("str_date")$str$to_date(strict = FALSE))
```

    #> shape: (4, 2)
    #> ┌────────────┬────────────┐
    #> │ str_date   ┆ date       │
    #> │ ---        ┆ ---        │
    #> │ str        ┆ date       │
    #> ╞════════════╪════════════╡
    #> │ 2009-01-02 ┆ 2009-01-02 │
    #> │ 2009-01-03 ┆ 2009-01-03 │
    #> │ 2009-1-4   ┆ 2009-01-04 │
    #> │ 2009 05 01 ┆ null       │
    #> └────────────┴────────────┘
