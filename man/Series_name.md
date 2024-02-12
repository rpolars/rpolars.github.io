

# Property: Name

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/series__series.R#L495)

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
