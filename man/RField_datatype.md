

# Get/set Field datatype

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/Field.R#L98)

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
