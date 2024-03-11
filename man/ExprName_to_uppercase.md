

# Make the root column name uppercase

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__name.R#L102)

## Description

Due to implementation constraints, this method can only be called as the
last expression in a chain.

## Usage

<pre><code class='language-R'>ExprName_to_uppercase()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(Alice = 1:3)$with_columns(pl$col("Alice")$name$to_uppercase())
```

    #> shape: (3, 2)
    #> ┌───────┬───────┐
    #> │ Alice ┆ ALICE │
    #> │ ---   ┆ ---   │
    #> │ i32   ┆ i32   │
    #> ╞═══════╪═══════╡
    #> │ 1     ┆ 1     │
    #> │ 2     ┆ 2     │
    #> │ 3     ┆ 3     │
    #> └───────┴───────┘
