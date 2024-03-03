

# Reverse a variable

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__expr.R#L979)

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
