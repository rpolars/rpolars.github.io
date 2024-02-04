

# Get/set Field name

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/Field.R#L79)

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
