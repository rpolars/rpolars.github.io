

# Create List DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/datatype.R#L287)

## Description

Create List DataType

## Usage

<pre><code class='language-R'>DataType_List(datatype = "unknown")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_List_:_datatype">datatype</code>
</td>
<td>
an inner DataType, default is "Unknown" (placeholder for when inner
DataType does not matter, e.g. as used in example)
</td>
</tr>
</table>

## Value

a list DataType with an inner DataType

## Examples

``` r
library(polars)

# some nested List
pl$List(pl$List(pl$Boolean))
```

    #> DataType: List(
    #>     List(
    #>         Boolean,
    #>     ),
    #> )

``` r
# check if some maybe_list is a List DataType
maybe_List = pl$List(pl$UInt64)
pl$same_outer_dt(maybe_List, pl$List())
```

    #> [1] TRUE
