

# Sort a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L916)

## Description

Sort a Series

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
If <code>TRUE</code>, place nulls values last.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_sort_:_in_place">in_place</code>
</td>
<td>
If <code>TRUE</code>, this will set the flag mutably and return NULL.
Remember to use <code>options(polars.strictly_immutable = FALSE)</code>
before using this parameter, otherwise an error will occur. If
<code>FALSE</code> (default), it will return a cloned Series with the
flag.
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

as_polars_series(c(1.5, NA, 1, NaN, Inf, -Inf))$sort()
```

    #> polars Series: shape: (6,)
    #> Series: '' [f64]
    #> [
    #>  null
    #>  -inf
    #>  1.0
    #>  1.5
    #>  inf
    #>  NaN
    #> ]

``` r
as_polars_series(c(1.5, NA, 1, NaN, Inf, -Inf))$sort(nulls_last = TRUE)
```

    #> polars Series: shape: (6,)
    #> Series: '' [f64]
    #> [
    #>  -inf
    #>  1.0
    #>  1.5
    #>  inf
    #>  NaN
    #>  null
    #> ]
