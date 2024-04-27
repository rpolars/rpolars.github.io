

# Subtract Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/series__series.R#L398)

## Description

Method equivalent of subtraction operator <code>series - other</code>.

## Usage

<pre><code class='language-R'>Series_sub(other)
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

as_polars_series(1:3)$sub(11:13)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  -10
    #>  -10
    #>  -10
    #> ]

``` r
as_polars_series(1:3)$sub(as_polars_series(11:13))
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  -10
    #>  -10
    #>  -10
    #> ]

``` r
as_polars_series(1:3)$sub(1L)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  1
    #>  2
    #> ]

``` r
1L - as_polars_series(1:3)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  -1
    #>  -2
    #> ]

``` r
as_polars_series(1:3) - 1L
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  1
    #>  2
    #> ]
