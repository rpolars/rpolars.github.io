

# Combine Data and Time

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__datetime.R#L126)

## Description

Create a naive Datetime from an existing Date/Datetime expression and a
Time. Each date/datetime in the first half of the interval is mapped to
the start of its bucket. Each date/datetime in the second half of the
interval is mapped to the end of its bucket.

## Usage

<pre><code class='language-R'>ExprDT_combine(tm, tu = "us")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_combine_:_tm">tm</code>
</td>
<td>
Expr or numeric or PTime, the number of epoch since or before(if
negative) the Date or tm is an Expr e.g. a column of DataType ‘Time’ or
something into an Expr.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_combine_:_tu">tu</code>
</td>
<td>
time unit of epochs, default is "us", if tm is a PTime, then tz passed
via PTime.
</td>
</tr>
</table>

## Details

The <code>tu</code> allows the following time time units the following
string language:

<ul>
<li>

1ns \# 1 nanosecond

</li>
<li>

1us \# 1 microsecond

</li>
<li>

1ms \# 1 millisecond

</li>
</ul>

## Value

Date/Datetime expr

## Examples

``` r
library(polars)

# Using pl$PTime
pl$lit(as.Date("2021-01-01"))$dt$combine(pl$PTime("02:34:12"))$to_series()
```

    #> polars Series: shape: (1,)
    #> Series: '' [datetime[ns]]
    #> [
    #>  2021-01-01 02:34:12
    #> ]

``` r
pl$lit(as.Date("2021-01-01"))$dt$combine(pl$PTime(3600 * 1.5, tu = "s"))$to_series()
```

    #> polars Series: shape: (1,)
    #> Series: '' [datetime[ns]]
    #> [
    #>  2021-01-01 01:30:00
    #> ]

``` r
pl$lit(as.Date("2021-01-01"))$dt$combine(pl$PTime(3600 * 1.5E6 + 123, tu = "us"))$to_series()
```

    #> polars Series: shape: (1,)
    #> Series: '' [datetime[ns]]
    #> [
    #>  2021-01-01 01:30:00.000123
    #> ]

``` r
# pass double and set tu manually
pl$lit(as.Date("2021-01-01"))$dt$combine(3600 * 1.5E6 + 123, tu = "us")$to_series()
```

    #> polars Series: shape: (1,)
    #> Series: '' [datetime[μs]]
    #> [
    #>  2021-01-01 01:30:00.000123
    #> ]

``` r
# if needed to convert back to R it is more intuitive to set a specific time zone
expr = pl$lit(as.Date("2021-01-01"))$dt$combine(3600 * 1.5E6 + 123, tu = "us")
expr$cast(pl$Datetime("us", "GMT"))$to_r()
```

    #> [1] "2021-01-01 01:30:00 GMT"
