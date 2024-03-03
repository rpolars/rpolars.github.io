

# Floor Divide Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L329)

## Description

Method equivalent of floor division operator <code>series %/%
other</code>.

## Usage

<pre><code class='language-R'>Series_floor_div(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_floor_div_:_other">other</code>
</td>
<td>
Series like object of numeric. Converted to Series by
<code>as_polars_series()</code> in this method.
</td>
</tr>
</table>

## Value

Series

## See Also

<ul>
<li>

Arithmetic operators

</li>
</ul>

## Examples

``` r
library(polars)

pl$Series(1:3)$floor_div(11:13)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  0
    #>  0
    #> ]

``` r
pl$Series(1:3)$floor_div(pl$Series(11:13))
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  0
    #>  0
    #> ]

``` r
pl$Series(1:3)$floor_div(1L)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]
