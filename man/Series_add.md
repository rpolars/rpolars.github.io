

# Add Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/series__series.R#L321)

## Description

Method equivalent of addition operator <code>series + other</code>.

## Usage

<pre><code class='language-R'>Series_add(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_add_:_other">other</code>
</td>
<td>
Series like object of numeric or string values. Converted to Series by
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
pl$Series("a")$add("-z")
```

    #> polars Series: shape: (1,)
    #> Series: '' [str]
    #> [
    #>  "a-z"
    #> ]
