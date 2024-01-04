
# Get/set Field datatype

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/Field.R#L98)

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
