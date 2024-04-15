

# Make the root column name lowercase

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__name.R#L89)

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
