

# Sort this Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L859)

## Description

Sort this Series

## Usage

<pre><code class='language-R'>Series_sort(descending = FALSE, nulls_last = FALSE, in_place = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_sort_:_descending">descending</code>
</td>
<td>
Sort in descending order.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_sort_:_nulls_last">nulls_last</code>
</td>
<td>
Place null values last instead of first.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_sort_:_in_place">in_place</code>
</td>
<td>
bool sort mutable in-place, breaks immutability If true will throw an
error unless this option has been set:
<code>options(polars.strictly_immutable = FALSE)</code>
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

pl$Series(c(1, NA, NaN, Inf, -Inf))$sort()
```

    #> polars Series: shape: (5,)
    #> Series: '' [f64]
    #> [
    #>  null
    #>  -inf
    #>  1.0
    #>  inf
    #>  NaN
    #> ]
