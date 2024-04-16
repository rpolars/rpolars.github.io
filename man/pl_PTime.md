

# Store Time in R

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/PTime.R#L70)

## Description

Store Time in R

## Usage

<pre><code class='language-R'>pl_PTime(x, tu = c("s", "ms", "us", "ns"), format = "%H:%M:%S")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_PTime_:_x">x</code>
</td>
<td>
an integer or double vector of n epochs since midnight OR a char vector
of char times passed to as.POSIXct converted to seconds.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_PTime_:_tu">tu</code>
</td>
<td>
timeunit either "s","ms","us","ns"
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_PTime_:_format">format</code>
</td>
<td>
a format string passed to as.POSIXct format via …
</td>
</tr>
</table>

## Details

PTime should probably be replaced with package nanotime or similar.

base R is missing encoding of Time since midnight "s" "ms", "us" and
"ns". The latter "ns" is the standard for the polars Time type.

Use PTime to convert R doubles and integers and use as input to polars
functions which needs a time.

Loosely inspired by data.table::ITime which is i32 only. PTime must
support polars native timeunit is nanoseconds. The R double(float64) can
imitate a i64 ns with full precision within the full range of 24 hours.

PTime does not have a time zone and always prints the time as is no
matter local machine time zone.

An essential difference between R and polars is R prints POSIXct/lt
without a timezone in local time. Polars prints Datetime without a
timezone label as is (GMT). For POSIXct/lt taged with a timexone(tzone)
and Datetime with a timezone(tz) the behavior is the same conversion is
intuitive.

It appears behavior of R timezones is subject to change a bit in R
4.3.0, see polars unit test test-expr_datetime.R/"pl$date_range Date
lazy/eager".

## Value

a PTime vector either double or integer, with class "PTime" and
attribute "tu" being either "s","ms","us" or "ns"

## Examples

``` r
library(polars)


# make PTime in all time units
pl$PTime(runif(5) * 3600 * 24 * 1E0, tu = "s")
```

    #> PTime [ double ]: number of epochs [ s ] since midnight
    #> [1] "04:33:11 val: 16391" "13:11:14 val: 47474" "11:05:10 val: 39910"
    #> [4] "03:07:17 val: 11237" "05:23:40 val: 19420"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E3, tu = "ms")
```

    #> PTime [ double ]: number of epochs [ ms ] since midnight
    #> [1] "00:39:26:810ms val: 2366810"  "04:35:51:875ms val: 16551875"
    #> [3] "22:22:42:819ms val: 80562819" "16:10:13:905ms val: 58213905"
    #> [5] "21:07:08:722ms val: 76028722"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E6, tu = "us")
```

    #> PTime [ double ]: number of epochs [ us ] since midnight
    #> [1] "22:50:42:505_853us val: 82242505853" "16:09:43:097_869us val: 58183097869"
    #> [3] "18:36:13:940_230us val: 66973940230" "05:40:57:242_106us val: 20457242106"
    #> [5] "08:09:56:266_664us val: 29396266664"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E9, tu = "ns")
```

    #> PTime [ double ]: number of epochs [ ns ] since midnight
    #> [1] "00:31:49:797_969_460ns val: 1909797969460" 
    #> [2] "00:33:25:494_553_595ns val: 2005494553595" 
    #> [3] "00:34:04:679_394_364ns val: 2044679394364" 
    #> [4] "09:42:35:818_766_355ns val: 34955818766355"
    #> [5] "08:31:32:473_212_629ns val: 30692473212629"

``` r
pl$PTime("23:59:59")
```

    #> PTime [ double ]: number of epochs [ s ] since midnight
    #> [1] "23:59:59 val: 86399"

``` r
as_polars_series(pl$PTime(runif(5) * 3600 * 24 * 1E0, tu = "s"))
```

    #> polars Series: shape: (5,)
    #> Series: '' [time]
    #> [
    #>  15:44:54
    #>  13:31:52
    #>  21:08:19
    #>  20:21:16
    #>  15:53:47
    #> ]

``` r
pl$lit(pl$PTime("23:59:59"))$to_series()
```

    #> polars Series: shape: (1,)
    #> Series: '' [time]
    #> [
    #>  23:59:59
    #> ]

``` r
pl$lit(pl$PTime("23:59:59"))$to_r()
```

    #> PTime [ double ]: number of epochs [ ns ] since midnight
    #> [1] "23:59:59:000_000_000ns val: 8.6399e+13"
