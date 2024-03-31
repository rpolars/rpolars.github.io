

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
    #> [1] "13:33:31 val: 48811" "06:08:50 val: 22130" "14:32:26 val: 52346"
    #> [4] "18:36:08 val: 66968" "00:48:42 val: 2922"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E3, tu = "ms")
```

    #> PTime [ double ]: number of epochs [ ms ] since midnight
    #> [1] "20:28:12:799ms val: 73692799" "07:11:18:070ms val: 25878070"
    #> [3] "17:41:35:889ms val: 63695889" "23:27:28:194ms val: 84448194"
    #> [5] "19:44:21:660ms val: 71061660"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E6, tu = "us")
```

    #> PTime [ double ]: number of epochs [ us ] since midnight
    #> [1] "08:52:55:008_923us val: 31975008923" "07:15:14:299_714us val: 26114299714"
    #> [3] "00:08:26:717_247us val: 506717247"   "06:01:47:532_971us val: 21707532971"
    #> [5] "20:43:01:509_688us val: 74581509688"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E9, tu = "ns")
```

    #> PTime [ double ]: number of epochs [ ns ] since midnight
    #> [1] "19:34:50:108_484_774ns val: 70490108484774"
    #> [2] "09:49:26:511_348_634ns val: 35366511348634"
    #> [3] "19:38:03:276_859_670ns val: 70683276859670"
    #> [4] "11:17:21:591_225_564ns val: 40641591225564"
    #> [5] "14:02:03:126_543_313ns val: 50523126543313"

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
    #>  03:17:58
    #>  17:50:57
    #>  14:10:02
    #>  02:10:00
    #>  16:31:20
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
