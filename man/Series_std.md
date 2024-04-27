

# Compute the standard deviation of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/series__series.R#L857)

## Description

Compute the standard deviation of a Series

## Usage

<pre><code class='language-R'>Series_std(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ddof">ddof</code>
</td>
<td>
Delta Degrees of Freedom: the divisor used in the calculation is N -
ddof, where N represents the number of elements. By default ddof is 1.
</td>
</tr>
</table>

## Value

A numeric value

## Examples

``` r
library(polars)

as_polars_series(1:10)$std()
```

    #> [1] 3.02765
