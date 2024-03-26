

# Multiply Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L401)

## Description

Method equivalent of multiplication operator <code>series \*
other</code>.

## Usage

<pre><code class='language-R'>Series_mul(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_mul_:_other">other</code>
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

as_polars_series(1:3)$mul(11:13)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  11
    #>  24
    #>  39
    #> ]

``` r
as_polars_series(1:3)$mul(as_polars_series(11:13))
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  11
    #>  24
    #>  39
    #> ]

``` r
as_polars_series(1:3)$mul(1L)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]
