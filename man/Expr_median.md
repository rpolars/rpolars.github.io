

# Get median value

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/after-wrappers.R#L20)

## Description

Get median value

## Usage

<pre><code class='language-R'>Expr_median()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1L, NA, 2L))$
  with_columns(median = pl$col("x")$median())
```

    #> shape: (3, 2)
    #> ┌──────┬────────┐
    #> │ x    ┆ median │
    #> │ ---  ┆ ---    │
    #> │ i32  ┆ f64    │
    #> ╞══════╪════════╡
    #> │ 1    ┆ 1.5    │
    #> │ null ┆ 1.5    │
    #> │ 2    ┆ 1.5    │
    #> └──────┴────────┘
