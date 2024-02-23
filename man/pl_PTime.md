

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
    #> [1] "21:55:52 val: 78952" "22:16:34 val: 80194" "23:04:07 val: 83047"
    #> [4] "09:32:04 val: 34324" "13:20:28 val: 48028"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E3, tu = "ms")
```

    #> PTime [ double ]: number of epochs [ ms ] since midnight
    #> [1] "01:18:24:526ms val: 4704526"  "23:33:41:703ms val: 84821703"
    #> [3] "05:02:58:282ms val: 18178282" "12:51:14:870ms val: 46274870"
    #> [5] "05:15:53:523ms val: 18953523"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E6, tu = "us")
```

    #> PTime [ double ]: number of epochs [ us ] since midnight
    #> [1] "01:09:14:963_462us val: 4154963462"  "03:06:42:563_115us val: 11202563115"
    #> [3] "05:57:16:677_771us val: 21436677771" "02:55:28:910_402us val: 10528910402"
    #> [5] "21:51:33:183_685us val: 78693183685"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E9, tu = "ns")
```

    #> PTime [ double ]: number of epochs [ ns ] since midnight
    #> [1] "12:35:25:492_434_203ns val: 45325492434203"
    #> [2] "16:51:56:609_072_685ns val: 60716609072685"
    #> [3] "02:50:28:188_557_177ns val: 10228188557177"
    #> [4] "11:31:39:394_599_348ns val: 41499394599348"
    #> [5] "00:12:44:092_958_718ns val: 764092958718"

``` r
pl$PTime("23:59:59")
```

    #> PTime [ double ]: number of epochs [ s ] since midnight
    #> [1] "23:59:59 val: 86399"

``` r
pl$Series(pl$PTime(runif(5) * 3600 * 24 * 1E0, tu = "s"))
```

    #> polars Series: shape: (5,)
    #> Series: '' [time]
    #> [
    #>  04:58:02
    #>  00:43:17
    #>  00:55:50
    #>  22:56:38
    #>  01:15:45
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
