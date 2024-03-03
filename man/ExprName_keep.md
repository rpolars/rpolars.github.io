

# Keep the original root name of the expression.

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__name.R#L47)

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
