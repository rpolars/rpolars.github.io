
# Convert Literal to Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__expr.R#L3448)

## Description

Collect an expression based on literals into a Series.

## Usage

<pre><code class='language-R'>Expr_to_series()
</code></pre>

## Value

Series

## Examples

``` r
library(polars)

pl$lit(1:5)$to_series()
```

    #> polars Series: shape: (5,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #>  5
    #> ]
