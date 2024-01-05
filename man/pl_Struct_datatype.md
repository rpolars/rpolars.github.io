
# Create Struct DataType

## Description

Struct DataType Constructor

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_Struct_datatype_:_datatype">datatype</code>
</td>
<td>
an inner DataType
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

# create a Struct-DataType
pl$List(pl$List(pl$Boolean))
```

    #> DataType: List(
    #>     List(
    #>         Boolean,
    #>     ),
    #> )

``` r
# Find any DataType via pl$dtypes
print(pl$dtypes)
```

    #> $Boolean
    #> DataType: Boolean
    #> 
    #> $UInt8
    #> DataType: UInt8
    #> 
    #> $UInt16
    #> DataType: UInt16
    #> 
    #> $UInt32
    #> DataType: UInt32
    #> 
    #> $UInt64
    #> DataType: UInt64
    #> 
    #> $Int8
    #> DataType: Int8
    #> 
    #> $Int16
    #> DataType: Int16
    #> 
    #> $Int32
    #> DataType: Int32
    #> 
    #> $Int64
    #> DataType: Int64
    #> 
    #> $Float32
    #> DataType: Float32
    #> 
    #> $Float64
    #> DataType: Float64
    #> 
    #> $String
    #> DataType: String
    #> 
    #> $Binary
    #> DataType: Binary
    #> 
    #> $Date
    #> DataType: Date
    #> 
    #> $Time
    #> DataType: Time
    #> 
    #> $Null
    #> DataType: Null
    #> 
    #> $Categorical
    #> DataType: Categorical(
    #>     None,
    #>     Physical,
    #> )
    #> 
    #> $Unknown
    #> DataType: Unknown
    #> 
    #> $Utf8
    #> DataType: String
    #> 
    #> $Datetime
    #> function(tu = "us", tz = NULL) {
    #>     if (!is.null(tz) && (!is_string(tz) || !tz %in% base::OlsonNames())) {
    #>       stop("Datetime: the tz '%s' is not a valid timezone string, see base::OlsonNames()", tz)
    #>     }
    #>     unwrap(.pr$DataType$new_datetime(tu, tz))
    #>   }
    #> <bytecode: 0x55c9e41fd620>
    #> <environment: namespace:polars>
    #> 
    #> $List
    #> function(datatype = "unknown") {
    #>     if (is.character(datatype) && length(datatype) == 1) {
    #>       datatype = .pr$DataType$new(datatype)
    #>     }
    #>     if (!inherits(datatype, "RPolarsDataType")) {
    #>       stop(paste(
    #>         "input for generating a list DataType must be another DataType",
    #>         "or an interpretable name thereof."
    #>       ))
    #>     }
    #>     .pr$DataType$new_list(datatype)
    #>   }
    #> <bytecode: 0x55c9e41e77b8>
    #> <environment: namespace:polars>
    #> 
    #> $Struct
    #> function(...) {
    #>     result({
    #>       largs = list2(...)
    #>       if (length(largs) >= 1 && is.list(largs[[1]])) {
    #>         largs = largs[[1]]
    #>         element_name = "list element"
    #>       } else {
    #>         element_name = "positional argument"
    #>       }
    #>       mapply(
    #>         names(largs) %||% character(length(largs)),
    #>         largs,
    #>         seq_along(largs),
    #>         FUN = \(name, arg, i) {
    #>           if (inherits(arg, "RPolarsDataType")) {
    #>             return(pl$Field(name, arg))
    #>           }
    #>           if (inherits(arg, "RPolarsRField")) {
    #>             return(arg)
    #>           }
    #>           stop(
    #>             "%s [%s] {name:'%s', value:%s} must either be a Field (pl$Field) or a named %s",
    #>             element_name, i, name, arg, "DataType see (pl$dtypes), see examples for pl$Struct()"
    #>           )
    #>         }, SIMPLIFY = FALSE
    #>       )
    #>     }) |>
    #>       and_then(DataType$new_struct) |>
    #>       unwrap("in pl$Struct:")
    #>   }
    #> <bytecode: 0x55c9e40cf9f8>
    #> <environment: namespace:polars>

``` r
# check if an element is any kind of Struct()
test = pl$Struct(pl$UInt64)
pl$same_outer_dt(test, pl$Struct())
```

    #> [1] TRUE

``` r
# `test` is a type of Struct, but it doesn't mean it is equal to an empty Struct
test == pl$Struct()
```

    #> [1] FALSE
