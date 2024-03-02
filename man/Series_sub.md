

# sub Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L309)

## Description

Series arithmetics

## Usage

<pre><code class='language-R'>Series_sub(other)

# S3 method for class 'RPolarsSeries'
s1 - s2
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_sub_:_other">other</code>
</td>
<td>
Series or into Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_sub_:_s1">s1</code>
</td>
<td>
lhs Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_sub_:_s2">s2</code>
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
