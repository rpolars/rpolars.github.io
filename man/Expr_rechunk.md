

# Rechunk memory layout

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/after-wrappers.R#L20)

## Description

Create a single chunk of memory for this Series.

## Usage

<pre><code class='language-R'>Expr_rechunk()
</code></pre>

## Details

See rechunk() explained here <code>docs_translations</code>.

## Value

Expr

## Examples

``` r
library(polars)

# get chunked lengths with/without rechunk
series_list = pl$DataFrame(list(a = 1:3, b = 4:6))$select(
  pl$col("a")$append(pl$col("b"))$alias("a_chunked"),
  pl$col("a")$append(pl$col("b"))$rechunk()$alias("a_rechunked")
)$get_columns()
lapply(series_list, \(x) x$chunk_lengths())
```

    #> $a_chunked
    #> [1] 3 3
    #> 
    #> $a_rechunked
    #> [1] 6
