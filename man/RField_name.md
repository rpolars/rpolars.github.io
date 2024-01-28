

# Get/set Field name

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/Field.R#L79)

## Description

Get/set Field name

## Usage

<pre><code class='language-R'>RField_name()
</code></pre>

## Examples

``` r
library(polars)

field = pl$Field("Cities", pl$String)
field$name
```

    #> [1] "Cities"

``` r
field$name = "CityPoPulations" #<- is fine too
field
```

    #> Field {
    #>     name: "CityPoPulations",
    #>     dtype: String,
    #> }
