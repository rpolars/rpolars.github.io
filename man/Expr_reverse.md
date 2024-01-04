
# Reverse a variable

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/expr__expr.R#L944)

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
