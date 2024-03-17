

# Create Array DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/datatype.R#L253)

## Description

The Array and List datatypes are very similar. The only difference is
that sub-arrays all have the same length while sublists can have
different lengths. Array methods can be accessed via the
<code style="white-space: pre;">$arr</code> subnamespace.

## Usage

<pre><code class='language-R'>DataType_Array(datatype = "unknown", width)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Array_:_datatype">datatype</code>
</td>
<td>
An inner DataType. The default is <code>“Unknown”</code> and is only a
placeholder for when inner DataType does not matter, e.g. as used in
example.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Array_:_width">width</code>
</td>
<td>
The length of the arrays.
</td>
</tr>
</table>

## Value

An array DataType with an inner DataType

## Examples

``` r
library(polars)

# basic Array
pl$Array(pl$Int32, 4)
```

    #> DataType: Array(
    #>     Int32,
    #>     4,
    #> )

``` r
# some nested Array
pl$Array(pl$Array(pl$Boolean, 3), 2)
```

    #> DataType: Array(
    #>     Array(
    #>         Boolean,
    #>         3,
    #>     ),
    #>     2,
    #> )
