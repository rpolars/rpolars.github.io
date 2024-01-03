
# Get/set Field datatype

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/Field.R#L98)

## Description

Get/set Field datatype

## Usage

<pre><code class='language-R'>RField_datatype()
</code></pre>

## Examples

``` r
library(polars)

field = pl$Field("Cities", pl$Utf8)
field$datatype
```

    #> DataType: Utf8

``` r
field$datatype = pl$Categorical #<- is fine too
field$datatype
```

    #> DataType: Categorical(
    #>     None,
    #>     Physical,
    #> )
