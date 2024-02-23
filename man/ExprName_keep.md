

# Keep the original root name of the expression.

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__name.R#L49)

## Description

Keep the original root name of the expression.

## Usage

<pre><code class='language-R'>ExprName_keep()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(list(alice = 1:3))$select(pl$col("alice")$alias("bob")$name$keep())
```

    #> shape: (3, 1)
    #> ┌───────┐
    #> │ alice │
    #> │ ---   │
    #> │ i32   │
    #> ╞═══════╡
    #> │ 1     │
    #> │ 2     │
    #> │ 3     │
    #> └───────┘
