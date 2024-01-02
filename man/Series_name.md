
# Property: Name

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/series__series.R#L502)

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
