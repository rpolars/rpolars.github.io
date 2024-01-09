
# add Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/series__series.R#L94)

## Description

Series arithmetics

## Usage

<pre><code class='language-R'>Series_add(other)

# S3 method for class 'RPolarsSeries'
s1 + s2
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_add_:_other">other</code>
</td>
<td>
Series or into Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_add_:_s1">s1</code>
</td>
<td>
lhs Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_add_:_s2">s2</code>
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

pl$Series(1:3)$add(11:13)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  12
    #>  14
    #>  16
    #> ]

``` r
pl$Series(1:3)$add(pl$Series(11:13))
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  12
    #>  14
    #>  16
    #> ]

``` r
pl$Series(1:3)$add(1L)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  2
    #>  3
    #>  4
    #> ]

``` r
1L + pl$Series(1:3)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  2
    #>  3
    #>  4
    #> ]

``` r
pl$Series(1:3) + 1L
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  2
    #>  3
    #>  4
    #> ]
