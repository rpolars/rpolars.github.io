
# List registered tables

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/sql.R#L175)

## Description

Return a character vector of the registered table names.

## Usage

<pre><code class='language-R'>SQLContext_tables()
</code></pre>

## Value

A character vector of the registered table names.

## Examples

``` r
library(polars)


ctx = pl$SQLContext()
ctx$tables()
```

    #> character(0)

``` r
ctx$register("df1", mtcars)
ctx$tables()
```

    #> [1] "df1"

``` r
ctx$register("df2", mtcars)
ctx$tables()
```

    #> [1] "df1" "df2"
