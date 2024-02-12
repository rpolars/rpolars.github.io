

# Compare Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/series__series.R#L194)

## Description

compare two Series

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
<code id="Series_compare_:_other">other</code>
</td>
<td>
A Series or something a Series can be created from
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_compare_:_op">op</code>
</td>
<td>
the chosen operator a String either: ‘equal’, ‘not_equal’, ‘lt’, ‘gt’,
‘lt_eq’ or ‘gt_eq’
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_compare_:_s1">s1</code>
</td>
<td>
lhs Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_compare_:_s2">s2</code>
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

pl$Series(1:5) == pl$Series(c(1:3, NA_integer_, 10L))
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
