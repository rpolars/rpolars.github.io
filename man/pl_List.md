
# Create List DataType

## Description

Create List DataType

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_List_:_datatype">datatype</code>
</td>
<td>
an inner DataType, default is "Unknown" (placeholder for when inner
DataType does not matter, e.g. as used in example)
</td>
</tr>
</table>

## Format

function

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
