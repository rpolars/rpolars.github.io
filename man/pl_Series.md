

# Create new Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/series__series.R#L312)

## Description

This function is a simple way to convert R vectors to the Series class
object. Internally, this function is a simple wrapper of
<code>as_polars_series()</code>.

## Usage

<pre><code class='language-R'>pl_Series(..., values = NULL, name = NULL, dtype = NULL, nan_to_null = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Treated as <code>values</code>, <code>name</code>, and
<code>dtype</code> in order. In future versions, the order of the
arguments will be changed to <code>pl$Series(name, values, dtype, …,
nan_to_null)</code> and <code>…</code> will be ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="values">values</code>
</td>
<td>
Object to convert into a polars Series. Passed to the <code>x</code>
argument in as_polars_series().
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="name">name</code>
</td>
<td>
A character to use as the name of the Series, or <code>NULL</code>
(default). Passed to the <code>name</code> argument in
as_polars_series().
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="dtype">dtype</code>
</td>
<td>
One of polars data type or <code>NULL</code>. If not <code>NULL</code>,
that data type is used to cast the Series created from the vector to a
specific data type internally.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="nan_to_null">nan_to_null</code>
</td>
<td>
If <code>TRUE</code>, <code>NaN</code> values contained in the Series
are replaced to <code>null</code>. Using the <code>$fill_nan()</code>
method internally.
</td>
</tr>
</table>

## Value

Series

## See Also

<ul>
<li>

<code>as_polars_series()</code>

</li>
</ul>

## Examples

``` r
library(polars)

# Constructing a Series by specifying name and values positionally (deprecated):
s = suppressWarnings(pl$Series(1:3, "a"))
s
```

    #> polars Series: shape: (3,)
    #> Series: 'a' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]

``` r
# Notice that the dtype is automatically inferred as a polars Int32:
s$dtype
```

    #> DataType: Int32

``` r
# Constructing a Series with a specific dtype:
s2 = pl$Series(values = 1:3, name = "a", dtype = pl$Float32)
s2
```

    #> polars Series: shape: (3,)
    #> Series: 'a' [f32]
    #> [
    #>  1.0
    #>  2.0
    #>  3.0
    #> ]
