

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
    #> [1] "14:47:02 val: 53222" "20:17:48 val: 73068" "05:00:59 val: 18059"
    #> [4] "01:25:13 val: 5113"  "03:40:16 val: 13216"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E3, tu = "ms")
```

    #> PTime [ double ]: number of epochs [ ms ] since midnight
    #> [1] "23:22:43:173ms val: 84163173" "02:52:53:900ms val: 10373900"
    #> [3] "13:32:13:580ms val: 48733580" "11:37:13:332ms val: 41833332"
    #> [5] "20:43:04:005ms val: 74584005"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E6, tu = "us")
```

    #> PTime [ double ]: number of epochs [ us ] since midnight
    #> [1] "20:50:38:122_138us val: 75038122138" "18:55:20:281_226us val: 68120281226"
    #> [3] "05:09:22:731_783us val: 18562731783" "17:27:42:925_855us val: 62862925855"
    #> [5] "15:48:56:655_566us val: 56936655566"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E9, tu = "ns")
```

    #> PTime [ double ]: number of epochs [ ns ] since midnight
    #> [1] "02:55:00:563_885_271ns val: 10500563885271"
    #> [2] "11:43:04:470_304_101ns val: 42184470304101"
    #> [3] "12:44:19:227_318_316ns val: 45859227318316"
    #> [4] "16:31:47:965_879_887ns val: 59507965879887"
    #> [5] "20:16:51:833_108_961ns val: 73011833108961"

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
    #>  21:30:58
    #>  19:02:20
    #>  11:01:56
    #>  08:15:47
    #>  08:24:48
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
