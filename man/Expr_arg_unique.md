

# Index of first unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

This finds the position of first occurrence of each unique value.

## Usage

<pre><code class='language-R'>Expr_arg_unique()
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
