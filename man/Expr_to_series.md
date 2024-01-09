
# Convert Literal to Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__expr.R#L3450)

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
