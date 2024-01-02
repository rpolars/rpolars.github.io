
# Create Datetime DataType

## Description

Datetime DataType constructor

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_Datetime_:_tu">tu</code>
</td>
<td>
string option either "ms", "us" or "ns"
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_Datetime_:_tz">tz</code>
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
