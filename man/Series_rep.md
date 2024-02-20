

# duplicate and concatenate a series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L971)

## Description

duplicate and concatenate a series

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
number of times to repeat
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_rep_:_rechunk">rechunk</code>
</td>
<td>
bool default true, reallocate object in memory. If FALSE the Series will
take up less space, If TRUE calculations might be faster.
</td>
</tr>
</table>

## Format

method

## Details

This function in not implemented in pypolars

## Value

bool

## Examples

``` r
library(polars)

pl$Series(1:2, "bob")$rep(3)
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
