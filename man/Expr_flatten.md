

# Explode a list or String Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/after-wrappers.R#L20)

## Description

This is an alias for
<code style="white-space: pre;">\<Expr\>$explode()</code>.

## Usage

<pre><code class='language-R'>Expr_flatten()
</code></pre>

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
df$select(pl$col("y")$flatten())
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
