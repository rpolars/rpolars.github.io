
# Keep the original root name of the expression.

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__name.R#L49)

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
