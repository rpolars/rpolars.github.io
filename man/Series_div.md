

# Divide Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L413)

## Description

Method equivalent of division operator <code>series / other</code>.

## Usage

<pre><code class='language-R'>Series_div(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="other">other</code>
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

as_polars_series(1:3)$div(11:13)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  0
    #>  0
    #> ]

``` r
as_polars_series(1:3)$div(as_polars_series(11:13))
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  0
    #>  0
    #> ]

``` r
as_polars_series(1:3)$div(1L)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]
