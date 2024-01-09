
# List registered tables

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/sql.R#L175)

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
