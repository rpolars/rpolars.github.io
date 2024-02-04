

# Get/set Field datatype

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/Field.R#L98)

## Description

Get/set Field datatype

## Usage

<pre><code class='language-R'>RField_datatype()
</code></pre>

## Examples

``` r
library(polars)

field = pl$Field("Cities", pl$String)
field$datatype
```

    #> DataType: String

``` r
field$datatype = pl$Categorical #<- is fine too
field$datatype
```

    #> DataType: Categorical(
    #>     None,
    #>     Physical,
    #> )
