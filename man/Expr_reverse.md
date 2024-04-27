

# Reverse a variable

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L918)

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
