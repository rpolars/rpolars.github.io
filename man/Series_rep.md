

# Duplicate and concatenate a series

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/series__series.R#L1018)

## Description

Note that this function doesn’t exist in Python Polars.

## Usage

<pre><code class='language-R'>Series_rep(n, rechunk = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_rep_:_n">n</code>
</td>
<td>
Number of times to repeat
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_rep_:_rechunk">rechunk</code>
</td>
<td>
If <code>TRUE</code> (default), reallocate object in memory which can
speed up some calculations. If <code>FALSE</code>, the Series will take
less space in memory.
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

as_polars_series(1:2, "bob")$rep(3)
```

    #> polars Series: shape: (6,)
    #> Series: 'bob' [i32]
    #> [
    #>  1
    #>  2
    #>  1
    #>  2
    #>  1
    #>  2
    #> ]
