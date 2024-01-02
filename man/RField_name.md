
# Get/set Field name

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/Field.R#L79)

## Description

Get/set Field name

## Usage

<pre><code class='language-R'>RField_name()
</code></pre>

## Examples

``` r
library(polars)

field = pl$Field("Cities", pl$Utf8)
field$name
```

    #> [1] "Cities"

``` r
field$name = "CityPoPulations" #<- is fine too
field
```

    #> Field {
    #>     name: "CityPoPulations",
    #>     dtype: Utf8,
    #> }
