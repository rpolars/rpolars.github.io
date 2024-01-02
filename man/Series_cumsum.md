
# Cumulative sum

## Description

Get an array with the cumulative sum computed at every element.

## Usage

<pre><code class='language-R'>Series_cum_sum(reverse = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_cumsum_:_reverse">reverse</code>
</td>
<td>
bool, default FALSE, if true roll over vector from back to forth
</td>
</tr>
</table>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
summing to prevent overflow issues.

## Value

Series

## Examples

``` r
library(polars)

pl$Series(c(1:2, NA, 3, NaN, 4, Inf))$cum_sum()
```

    #> polars Series: shape: (7,)
    #> Series: '' [f64]
    #> [
    #>  1.0
    #>  3.0
    #>  null
    #>  6.0
    #>  NaN
    #>  NaN
    #>  NaN
    #> ]

``` r
pl$Series(c(1:2, NA, 3, Inf, 4, -Inf, 5))$cum_sum()
```

    #> polars Series: shape: (8,)
    #> Series: '' [f64]
    #> [
    #>  1.0
    #>  3.0
    #>  null
    #>  6.0
    #>  inf
    #>  inf
    #>  NaN
    #>  NaN
    #> ]
