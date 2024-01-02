
# strftime

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__datetime.R#L156)

## Description

Format Date/Datetime with a formatting rule. See
<code style="white-space: pre;">chrono strftime/strptime
\<https://docs.rs/chrono/latest/chrono/format/strftime/index.html\></code>\_.

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_strftime_:_format">format</code>
</td>
<td>
string format very much like in R passed to chrono
</td>
</tr>
</table>

## Format

function

## Value

Date/Datetime expr

## Examples

``` r
library(polars)

pl$lit(as.POSIXct("2021-01-02 12:13:14", tz = "GMT"))$dt$strftime("this is the year: %Y")$to_r()
```

    #> [1] "this is the year: 2021"
