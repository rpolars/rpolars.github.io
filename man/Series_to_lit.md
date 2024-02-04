

# Series to Literal

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L994)

## Description

convert Series to literal to perform modification and return

## Usage

<pre><code class='language-R'>Series_to_lit()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

(
  pl$Series(list(1:1, 1:2, 1:3, 1:4))
  $print()
  $to_lit()
  $list$len()
  $sum()
  $cast(pl$dtypes$Int8)
  $to_series()
)
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
