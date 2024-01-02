
# Std

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/series__series.R#L680)

## Description

Aggregate the columns of this Series to their standard deviation.

## Usage

<pre><code class='language-R'>Series_std(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_std_:_ddof">ddof</code>
</td>
<td>
integer Delta Degrees of Freedom: the divisor used in the calculation is
N - ddof, where N represents the number of elements. By default ddof is
1.
</td>
</tr>
</table>

## Value

A new <code>Series</code> object with applied aggregation.

## Examples

``` r
library(polars)

pl$Series(1:10)$std()
```

    #> [1] 3.02765
