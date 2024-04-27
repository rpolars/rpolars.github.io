

# Duplicate and concatenate a series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/series__series.R#L1018)

## Description

Note that this function doesn’t exist in Python Polars.

## Usage

<pre><code class='language-R'>Series_rep(n, rechunk = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
Number of times to repeat
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="rechunk">rechunk</code>
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
