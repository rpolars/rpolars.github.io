

# Keep the original root name of the expression.

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__name.R#L47)

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
