

# Keep the original root name of the expression.

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__name.R#L49)

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
