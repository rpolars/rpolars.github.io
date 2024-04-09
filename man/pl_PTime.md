

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
    #> [1] "21:30:08 val: 77408" "10:16:41 val: 37001" "07:15:12 val: 26112"
    #> [4] "13:44:38 val: 49478" "08:58:01 val: 32281"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E3, tu = "ms")
```

    #> PTime [ double ]: number of epochs [ ms ] since midnight
    #> [1] "09:01:26:198ms val: 32486198" "00:43:22:300ms val: 2602300" 
    #> [3] "15:53:18:413ms val: 57198413" "20:30:14:700ms val: 73814700"
    #> [5] "14:50:21:063ms val: 53421063"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E6, tu = "us")
```

    #> PTime [ double ]: number of epochs [ us ] since midnight
    #> [1] "06:19:29:341_152us val: 22769341152" "04:27:44:641_550us val: 16064641550"
    #> [3] "21:03:34:403_866us val: 75814403866" "02:21:35:329_982us val: 8495329982" 
    #> [5] "08:19:38:800_197us val: 29978800197"

``` r
pl$PTime(runif(5) * 3600 * 24 * 1E9, tu = "ns")
```

    #> PTime [ double ]: number of epochs [ ns ] since midnight
    #> [1] "05:46:43:911_077_231ns val: 20803911077231"
    #> [2] "11:32:44:121_063_798ns val: 41564121063798"
    #> [3] "23:05:56:671_504_676ns val: 83156671504676"
    #> [4] "04:49:25:133_853_256ns val: 17365133853256"
    #> [5] "17:35:10:768_648_982ns val: 63310768648982"

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
    #>  04:47:28
    #>  01:34:34
    #>  00:29:44
    #>  17:22:53
    #>  00:18:20
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
