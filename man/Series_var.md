

# Compute the variance of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L847)

## Description

Compute the variance of a Series

## Usage

<pre><code class='language-R'>Series_var(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_var_:_ddof">ddof</code>
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

as_polars_series(1:10)$var()
```

    #> [1] 9.166667
