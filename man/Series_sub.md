

# Subtract Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L340)

## Description

Method equivalent of subtraction operator <code>series - other</code>.

## Usage

<pre><code class='language-R'>Series_sub(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_sub_:_other">other</code>
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

pl$Series(1:3)$sub(11:13)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  -10
    #>  -10
    #>  -10
    #> ]

``` r
pl$Series(1:3)$sub(pl$Series(11:13))
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  -10
    #>  -10
    #>  -10
    #> ]

``` r
pl$Series(1:3)$sub(1L)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  1
    #>  2
    #> ]

``` r
1L - pl$Series(1:3)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  -1
    #>  -2
    #> ]

``` r
pl$Series(1:3) - 1L
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  0
    #>  1
    #>  2
    #> ]
