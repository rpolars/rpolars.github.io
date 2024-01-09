
# rem Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L180)

## Description

Series arithmetics, remainder

## Usage

<pre><code class='language-R'>Series_rem(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_rem_:_other">other</code>
</td>
<td>
Series or into Series
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

pl$Series(1:4)$rem(2L)
```

    #> polars Series: shape: (4,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  0
    #>  1
    #>  0
    #> ]

``` r
pl$Series(1:3)$rem(pl$Series(11:13))
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]

``` r
pl$Series(1:3)$rem(1L)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  0
    #>  0
    #> ]
