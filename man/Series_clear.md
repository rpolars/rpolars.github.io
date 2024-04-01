

# Create an empty or n-row null-filled copy of the Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L1103)

## Description

Returns a n-row null-filled Series with an identical schema.
<code>n</code> can be greater than the current number of values in the
Series.

## Usage

<pre><code class='language-R'>Series_clear(n = 0)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_clear_:_n">n</code>
</td>
<td>
Number of (null-filled) rows to return in the cleared frame.
</td>
</tr>
</table>

## Value

A n-value null-filled Series with an identical schema

## Examples

``` r
library(polars)

s = pl$Series(name = "a", values = 1:3)

s$clear()
```

    #> polars Series: shape: (0,)
    #> Series: 'a' [i32]
    #> [
    #> ]

``` r
s$clear(n = 5)
```

    #> polars Series: shape: (5,)
    #> Series: 'a' [i32]
    #> [
    #>  null
    #>  null
    #>  null
    #>  null
    #>  null
    #> ]
