
# Property: Name

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/series__series.R#L501)

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
