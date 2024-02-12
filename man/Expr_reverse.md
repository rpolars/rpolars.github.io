

# Reverse a variable

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/expr__expr.R#L917)

## Description

Reverse a variable

## Usage

<pre><code class='language-R'>Expr_reverse()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(list(a = 1:5))$select(pl$col("a")$reverse())
```

    #> shape: (5, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 5   │
    #> │ 4   │
    #> │ 3   │
    #> │ 2   │
    #> │ 1   │
    #> └─────┘
