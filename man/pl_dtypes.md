

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

    #>  [1] "Array"       "Binary"      "Boolean"     "Categorical" "Date"       
    #>  [6] "Datetime"    "Duration"    "Enum"        "Float32"     "Float64"    
    #> [11] "Int16"       "Int32"       "Int64"       "Int8"        "List"       
    #> [16] "Null"        "String"      "Struct"      "Time"        "UInt16"     
    #> [21] "UInt32"      "UInt64"      "UInt8"       "Unknown"     "Utf8"

``` r
pl$dtypes$Float64
```

    #> DataType: Float64

``` r
pl$dtypes$String
```

    #> DataType: String

``` r
pl$List(pl$List(pl$UInt64))
```

    #> DataType: List(
    #>     List(
    #>         UInt64,
    #>     ),
    #> )

``` r
pl$Struct(pl$Field("CityNames", pl$String))
```

    #> DataType: Struct(
    #>     [
    #>         Field {
    #>             name: "CityNames",
    #>             dtype: String,
    #>         },
    #>     ],
    #> )

``` r
# The function changes type from Int32 to String
# Specifying the output DataType: String solves the problem
as_polars_series(1:4)$map_elements(\(x) letters[x], datatype = pl$dtypes$String)
```

    #> polars Series: shape: (4,)
    #> Series: '_apply' [str]
    #> [
    #>  "a"
    #>  "b"
    #>  "c"
    #>  "d"
    #> ]
