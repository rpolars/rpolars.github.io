
# Get/set Field datatype

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/Field.R#L98)

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
