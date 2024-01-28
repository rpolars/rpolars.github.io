

# Property: Name

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L495)

## Description

Get name of Series

## Usage

<pre><code class='language-R'>Series_name()
</code></pre>

## Value

String the name

## Examples

``` r
library(polars)

pl$Series(1:3, name = "alice")$name
```

    #> [1] "alice"
