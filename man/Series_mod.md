

# Modulo Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/series__series.R#L458)

## Description

Method equivalent of modulo operator <code>series %% other</code>.

## Usage

<pre><code class='language-R'>Series_mod(other)
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

as_polars_series(1:4)$mod(2L)
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
as_polars_series(1:3)$mod(as_polars_series(11:13))
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]

``` r
as_polars_series(1:3)$mod(1L)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  0
    #>  0
    #> ]
