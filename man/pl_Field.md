

# Create Field

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/Field.R#L42)

## Description

A Field is composed of a name and a data type. Fields are used in
Structs-datatypes and Schemas to represent everything of the
Series/Column except the raw values.

## Usage

<pre><code class='language-R'>pl_Field(name, datatype)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="name">name</code>
</td>
<td>
Field name
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="datatype">datatype</code>
</td>
<td>
DataType
</td>
</tr>
</table>

## Value

An RPolarsRField object containing its name and its data type.

## Active Bindings

<h4>
datatype
</h4>

<code style="white-space: pre;">$datatype</code> returns the data type
of the Field.

<code style="white-space: pre;">$datatype = \<RPolarsDataType\></code>
sets the data type of the Field.

<h4>
name
</h4>

<code style="white-space: pre;">$name</code> returns the name of the
Field.

<code style="white-space: pre;">$name = “new_name”</code> sets the name
of the Field.

## Examples

``` r
library(polars)

field = pl$Field("city_names", pl$String)

field
```

    #> Field {
    #>     name: "city_names",
    #>     dtype: String,
    #> }

``` r
field$datatype
```

    #> DataType: String

``` r
field$name
```

    #> [1] "city_names"

``` r
# Set the new data type
field$datatype = pl$Categorical()
field$datatype
```

    #> DataType: Categorical(
    #>     None,
    #>     Physical,
    #> )

``` r
# Set the new name
field$name = "CityPoPulations"
field
```

    #> Field {
    #>     name: "CityPoPulations",
    #>     dtype: Categorical(
    #>         None,
    #>         Physical,
    #>     ),
    #> }
