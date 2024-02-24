

# To polars Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/as_polars.R#L321)

## Description

<code>as_polars_series()</code> is a generic function that converts an R
object to a polars Series. It is basically a wrapper for pl$Series().

## Usage

<pre><code class='language-R'>as_polars_series(x, name = NULL, ...)

# Default S3 method:
as_polars_series(x, name = NULL, ...)

# S3 method for class 'RPolarsSeries'
as_polars_series(x, name = NULL, ...)

# S3 method for class 'RPolarsExpr'
as_polars_series(x, name = NULL, ...)

# S3 method for class 'RPolarsThen'
as_polars_series(x, name = NULL, ...)

# S3 method for class 'RPolarsChainedThen'
as_polars_series(x, name = NULL, ...)

# S3 method for class 'POSIXlt'
as_polars_series(x, name = NULL, ...)

# S3 method for class 'data.frame'
as_polars_series(x, name = NULL, ...)

# S3 method for class 'vctrs_rcrd'
as_polars_series(x, name = NULL, ...)

# S3 method for class 'Array'
as_polars_series(x, name = NULL, ..., rechunk = TRUE)

# S3 method for class 'ChunkedArray'
as_polars_series(x, name = NULL, ..., rechunk = TRUE)

# S3 method for class 'nanoarrow_array'
as_polars_series(x, name = NULL, ...)

# S3 method for class 'nanoarrow_array_stream'
as_polars_series(x, name = NULL, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_series_:_x">x</code>
</td>
<td>
Object to convert into a polars Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_series_:_name">name</code>
</td>
<td>
A string to use as the name of the Series. If <code>NULL</code>
(default), the name of <code>x</code> is used or an unnamed Series is
created.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_series_:_...">…</code>
</td>
<td>
Additional arguments passed to methods.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_series_:_rechunk">rechunk</code>
</td>
<td>
A logical flag (default <code>TRUE</code>). Make sure that all data is
in contiguous memory.
</td>
</tr>
</table>

## Value

a Series

## Examples

``` r
library(polars)

as_polars_series(1:4)
```

    #> polars Series: shape: (4,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #> ]

``` r
as_polars_series(list(1:4))
```

    #> polars Series: shape: (1,)
    #> Series: '' [list[i32]]
    #> [
    #>  [1, 2, … 4]
    #> ]

``` r
as_polars_series(data.frame(a = 1:4))
```

    #> polars Series: shape: (4,)
    #> Series: '' [struct[1]]
    #> [
    #>  {1}
    #>  {2}
    #>  {3}
    #>  {4}
    #> ]

``` r
as_polars_series(pl$Series(1:4, name = "foo"))
```

    #> polars Series: shape: (4,)
    #> Series: 'foo' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #> ]

``` r
as_polars_series(pl$lit(1:4))
```

    #> polars Series: shape: (4,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #> ]
