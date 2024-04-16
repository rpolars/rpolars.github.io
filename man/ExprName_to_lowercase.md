

# Make the root column name lowercase

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__name.R#L89)

## Description

Due to implementation constraints, this method can only be called as the
last expression in a chain.

## Usage

<pre><code class='language-R'>ExprName_to_lowercase()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(Alice = 1:3)$with_columns(pl$col("Alice")$name$to_lowercase())
```

    #> shape: (3, 2)
    #> ┌───────┬───────┐
    #> │ Alice ┆ alice │
    #> │ ---   ┆ ---   │
    #> │ i32   ┆ i32   │
    #> ╞═══════╪═══════╡
    #> │ 1     ┆ 1     │
    #> │ 2     ┆ 2     │
    #> │ 3     ┆ 3     │
    #> └───────┴───────┘
