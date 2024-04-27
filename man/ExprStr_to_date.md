

# Convert a String column into a Date column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L137)

## Description

Convert a String column into a Date column

## Usage

<pre><code class='language-R'>ExprStr_to_date(format = NULL, ..., strict = TRUE, exact = TRUE, cache = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="format">format</code>
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
<code id="...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if a single string cannot
be parsed. If <code>FALSE</code>, produce a polars <code>null</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="exact">exact</code>
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
<code id="cache">cache</code>
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
<code>“%Y-%m-%d”</code>. If <code>NULL</code> (default), the format is
inferred from the data.

## Value

Expr of Date type

## See Also

<ul>
<li>

<code>\<Expr\>$str$strptime()</code>

</li>
</ul>

## Examples

``` r
library(polars)

s = as_polars_series(c("2020/01/01", "2020/02/01", "2020/03/01"))

s$str$to_date()
```

    #> polars Series: shape: (3,)
    #> Series: '' [date]
    #> [
    #>  2020-01-01
    #>  2020-02-01
    #>  2020-03-01
    #> ]

``` r
# by default, this errors if some values cannot be converted
s = as_polars_series(c("2020/01/01", "2020 02 01", "2020-03-01"))
try(s$str$to_date())
```

    #> Error : Execution halted with the following contexts
    #>    0: In R: in $select()
    #>    0: During function call [.main()]
    #>    1: Encountered the following error in Rust-Polars:
    #>          conversion from `str` to `date` failed in column '' for 1 out of 3 values: ["2020 02 01"]
    #> 
    #>       You might want to try:
    #>       - setting `strict=False` to set values that cannot be converted to `null`
    #>       - using `str.strptime`, `str.to_date`, or `str.to_datetime` and providing a format string

``` r
s$str$to_date(strict = FALSE)
```

    #> polars Series: shape: (3,)
    #> Series: '' [date]
    #> [
    #>  2020-01-01
    #>  null
    #>  2020-03-01
    #> ]
