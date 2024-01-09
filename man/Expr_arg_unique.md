
# Index of first unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

This finds the position of first occurrence of each unique value.

## Usage

<pre><code class='language-R'>Expr_arg_unique
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$select(pl$lit(c(1:2, 1:3))$arg_unique())
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │     │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 0   │
    #> │ 1   │
    #> │ 4   │
    #> └─────┘
