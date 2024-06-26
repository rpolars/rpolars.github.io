

# Compare Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L494)

## Description

Check the (in)equality of two Series.

## Usage

<pre><code class='language-R'>Series_compare(other, op)

# S3 method for class 'RPolarsSeries'
s1 == s2

# S3 method for class 'RPolarsSeries'
s1 != s2

# S3 method for class 'RPolarsSeries'
s1 &lt; s2

# S3 method for class 'RPolarsSeries'
s1 &gt; s2

# S3 method for class 'RPolarsSeries'
s1 &lt;= s2

# S3 method for class 'RPolarsSeries'
s1 &gt;= s2
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="other">other</code>
</td>
<td>
A Series or something a Series can be created from
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="op">op</code>
</td>
<td>
The chosen operator, must be one of <code>“equal”</code>,
<code>“not_equal”</code>, <code>“lt”</code>, <code>“gt”</code>,
<code>“lt_eq”</code> or <code>“gt_eq”</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="s1">s1</code>
</td>
<td>
lhs Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="s2">s2</code>
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

# We can either use `compare()`...
as_polars_series(1:5)$compare(as_polars_series(c(1:3, NA_integer_, 10L)), op = "equal")
```

    #> polars Series: shape: (5,)
    #> Series: '' [bool]
    #> [
    #>  true
    #>  true
    #>  true
    #>  null
    #>  false
    #> ]

``` r
# ... or the more classic way
as_polars_series(1:5) == as_polars_series(c(1:3, NA_integer_, 10L))
```

    #> polars Series: shape: (5,)
    #> Series: '' [bool]
    #> [
    #>  true
    #>  true
    #>  true
    #>  null
    #>  false
    #> ]
