

# Convert a Series to literal

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L1052)

## Description

Convert a Series to literal

## Usage

<pre><code class='language-R'>Series_to_lit()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

as_polars_series(list(1:1, 1:2, 1:3, 1:4))$
  print()$
  to_lit()$
  list$len()$
  sum()$
  cast(pl$dtypes$Int8)$
  to_series()
```

    #> shape: (4,)
    #> Series: '' [list[i32]]
    #> [
    #>  [1]
    #>  [1, 2]
    #>  [1, 2, 3]
    #>  [1, 2, … 4]
    #> ]

    #> polars Series: shape: (1,)
    #> Series: '' [i8]
    #> [
    #>  10
    #> ]
