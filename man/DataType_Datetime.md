

# Create Datetime DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/datatype.R#L175)

## Description

Datetime DataType constructor

## Usage

<pre><code class='language-R'>DataType_Datetime(tu = "us", tz = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Datetime_:_tu">tu</code>
</td>
<td>
string option either "ms", "us" or "ns"
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Datetime_:_tz">tz</code>
</td>
<td>
string the Time Zone, see details
</td>
</tr>
</table>

## Format

function

## Details

all allowed TimeZone designations can be found in
<code>base::OlsonNames()</code>

## Value

Datetime DataType

## Examples

``` r
library(polars)

pl$Datetime("ns", "Pacific/Samoa")
```

    #> DataType: Datetime(
    #>     Nanoseconds,
    #>     Some(
    #>         "Pacific/Samoa",
    #>     ),
    #> )
