

# Create Struct DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/datatype.R#L203)

## Description

Struct DataType Constructor

## Usage

<pre><code class='language-R'>DataType_Struct(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Struct_:_...">…</code>
</td>
<td>
RPolarsDataType objects
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
pl$Struct(pl$Boolean)
```

    #> DataType: Struct(
    #>     [
    #>         Field {
    #>             name: "",
    #>             dtype: Boolean,
    #>         },
    #>     ],
    #> )

``` r
pl$Struct(foo = pl$Int32, bar = pl$Float64)
```

    #> DataType: Struct(
    #>     [
    #>         Field {
    #>             name: "foo",
    #>             dtype: Int32,
    #>         },
    #>         Field {
    #>             name: "bar",
    #>             dtype: Float64,
    #>         },
    #>     ],
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
    #>   if (!is.null(tz) && (!is_string(tz) || !tz %in% base::OlsonNames())) {
    #>     stop("Datetime: the tz '%s' is not a valid timezone string, see base::OlsonNames()", tz)
    #>   }
    #>   unwrap(.pr$DataType$new_datetime(tu, tz))
    #> }
    #> <bytecode: 0x55e965a71118>
    #> <environment: namespace:polars>
    #> 
    #> $Array
    #> function(datatype = "unknown", width) {
    #>   if (is.character(datatype) && length(datatype) == 1) {
    #>     datatype = .pr$DataType$new(datatype)
    #>   }
    #>   if (!inherits(datatype, "RPolarsDataType")) {
    #>     stop(paste(
    #>       "input for generating a array DataType must be another DataType",
    #>       "or an interpretable name thereof."
    #>     ))
    #>   }
    #>   .pr$DataType$new_array(datatype, width) |>
    #>     unwrap("in pl$Array():")
    #> }
    #> <bytecode: 0x55e965a3ad50>
    #> <environment: namespace:polars>
    #> 
    #> $List
    #> function(datatype = "unknown") {
    #>   if (is.character(datatype) && length(datatype) == 1) {
    #>     datatype = .pr$DataType$new(datatype)
    #>   }
    #>   if (!inherits(datatype, "RPolarsDataType")) {
    #>     stop(paste(
    #>       "input for generating a list DataType must be another DataType",
    #>       "or an interpretable name thereof."
    #>     ))
    #>   }
    #>   .pr$DataType$new_list(datatype)
    #> }
    #> <bytecode: 0x55e9659db090>
    #> <environment: namespace:polars>
    #> 
    #> $Struct
    #> function(...) {
    #>   result({
    #>     largs = list2(...)
    #>     if (length(largs) >= 1 && is.list(largs[[1]])) {
    #>       largs = largs[[1]]
    #>       element_name = "list element"
    #>     } else {
    #>       element_name = "positional argument"
    #>     }
    #>     mapply(
    #>       names(largs) %||% character(length(largs)),
    #>       largs,
    #>       seq_along(largs),
    #>       FUN = \(name, arg, i) {
    #>         if (inherits(arg, "RPolarsDataType")) {
    #>           return(pl$Field(name, arg))
    #>         }
    #>         if (inherits(arg, "RPolarsRField")) {
    #>           return(arg)
    #>         }
    #>         stop(sprintf(
    #>           "%s [%s] {name:'%s', value:%s} must either be a Field (pl$Field) or a named DataType",
    #>           element_name, i, name, arg
    #>         ))
    #>       }, SIMPLIFY = FALSE
    #>     )
    #>   }) |>
    #>     and_then(DataType$new_struct) |>
    #>     unwrap("in pl$Struct:")
    #> }
    #> <bytecode: 0x55e9659b69c8>
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
