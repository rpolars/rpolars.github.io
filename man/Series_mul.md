

# mul Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L160)

## Description

Series arithmetics

## Usage

<pre><code class='language-R'>Series_mul(other)

# S3 method for class 'RPolarsSeries'
s1 * s2
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_mul_:_other">other</code>
</td>
<td>
Series or into Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_mul_:_s1">s1</code>
</td>
<td>
lhs Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_mul_:_s2">s2</code>
</td>
<td>
rhs Series or any into Series
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

pl$Series(1:3)$mul(11:13)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  11
    #>  24
    #>  39
    #> ]

``` r
pl$Series(1:3)$mul(pl$Series(11:13))
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  11
    #>  24
    #>  39
    #> ]

``` r
pl$Series(1:3)$mul(1L)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]

``` r
2L * pl$Series(1:3)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  2
    #>  4
    #>  6
    #> ]

``` r
pl$Series(1:3) * 2L
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  2
    #>  4
    #>  6
    #> ]
