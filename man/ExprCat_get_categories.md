

# Get the categories stored in this data type

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__categorical.R#L48)

## Description

Get the categories stored in this data type

## Usage

<pre><code class='language-R'>ExprCat_get_categories()
</code></pre>

## Value

A polars DataFrame with the categories for each categorical Series.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  cats = factor(c("z", "z", "k", "a", "b")),
  vals = factor(c(3, 1, 2, 2, 3))
)
df
```

    #> shape: (5, 2)
    #> ┌──────┬──────┐
    #> │ cats ┆ vals │
    #> │ ---  ┆ ---  │
    #> │ cat  ┆ cat  │
    #> ╞══════╪══════╡
    #> │ z    ┆ 3    │
    #> │ z    ┆ 1    │
    #> │ k    ┆ 2    │
    #> │ a    ┆ 2    │
    #> │ b    ┆ 3    │
    #> └──────┴──────┘

``` r
df$select(
  pl$col("cats")$cat$get_categories()
)
```

    #> shape: (4, 1)
    #> ┌──────┐
    #> │ cats │
    #> │ ---  │
    #> │ str  │
    #> ╞══════╡
    #> │ z    │
    #> │ k    │
    #> │ a    │
    #> │ b    │
    #> └──────┘

``` r
df$select(
  pl$col("vals")$cat$get_categories()
)
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ vals │
    #> │ ---  │
    #> │ str  │
    #> ╞══════╡
    #> │ 3    │
    #> │ 1    │
    #> │ 2    │
    #> └──────┘
