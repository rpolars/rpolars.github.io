

# Create Field

## Description

A Field is composed of a name and a DataType. Fields are used in
Structs- datatypes and Schemas to represent everything of the
Series/Column except the raw values.

## Usage

<pre><code class='language-R'>pl_Field(name, datatype)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="RField_class_:_name">name</code>
</td>
<td>
Field name
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="RField_class_:_datatype">datatype</code>
</td>
<td>
DataType
</td>
</tr>
</table>

## Value

A object of with DataType <code>“RField”</code> containing its name and
its DataType.

## Examples

``` r
library(polars)

pl$Field("city_names", pl$String)
```

    #> Field {
    #>     name: "city_names",
    #>     dtype: String,
    #> }
