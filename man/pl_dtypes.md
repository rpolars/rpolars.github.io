
# DataTypes (RPolarsDataType)

## Description

<code>DataType</code> any polars type (ported so far)

## Value

not applicable

## Examples

``` r
library(polars)

print(ls(pl$dtypes))
```

    #>  [1] "Binary"      "Boolean"     "Categorical" "Date"        "Datetime"   
    #>  [6] "Float32"     "Float64"     "Int16"       "Int32"       "Int64"      
    #> [11] "Int8"        "List"        "Null"        "Struct"      "Time"       
    #> [16] "UInt16"      "UInt32"      "UInt64"      "UInt8"       "Unknown"    
    #> [21] "Utf8"

``` r
pl$dtypes$Float64
```

    #> DataType: Float64

``` r
pl$dtypes$Utf8
```

    #> DataType: Utf8

``` r
pl$List(pl$List(pl$UInt64))
```

    #> DataType: List(
    #>     List(
    #>         UInt64,
    #>     ),
    #> )

``` r
pl$Struct(pl$Field("CityNames", pl$Utf8))
```

    #> DataType: Struct(
    #>     [
    #>         Field {
    #>             name: "CityNames",
    #>             dtype: Utf8,
    #>         },
    #>     ],
    #> )

``` r
# The function changes type from Integer(Int32)[Integers] to char(Utf8)[Strings]
# specifying the output DataType: Utf8 solves the problem
pl$Series(1:4)$map_elements(\(x) letters[x], datatype = pl$dtypes$Utf8)
```

    #> polars Series: shape: (4,)
    #> Series: '_apply' [str]
    #> [
    #>  "a"
    #>  "b"
    #>  "c"
    #>  "d"
    #> ]
