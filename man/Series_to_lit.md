
# Series to Literal

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/series__series.R#L986)

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
  $list$lengths()
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
