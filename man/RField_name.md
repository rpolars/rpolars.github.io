
# Get/set Field name

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/Field.R#L79)

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
