

# Explode a list or String Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

## Description

This means that every item is expanded to a new row.

## Usage

<pre><code class='language-R'>Expr_explode()
</code></pre>

## Details

Categorical values are not supported.

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(x = c("abc", "ab"), y = c(list(1:3), list(3:5)))
df
```

    #> shape: (2, 2)
    #> ┌─────┬───────────┐
    #> │ x   ┆ y         │
    #> │ --- ┆ ---       │
    #> │ str ┆ list[i32] │
    #> ╞═════╪═══════════╡
    #> │ abc ┆ [1, 2, 3] │
    #> │ ab  ┆ [3, 4, 5] │
    #> └─────┴───────────┘

``` r
df$select(pl$col("y")$explode())
```

    #> shape: (6, 1)
    #> ┌─────┐
    #> │ y   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> │ 3   │
    #> │ 4   │
    #> │ 5   │
    #> └─────┘
