

# Count missing values

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Count missing values

## Usage

<pre><code class='language-R'>Expr_null_count()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(NA, "a", NA, "b"))$
  with_columns(n_missing = pl$col("x")$null_count())
```

    #> shape: (4, 2)
    #> ┌──────┬───────────┐
    #> │ x    ┆ n_missing │
    #> │ ---  ┆ ---       │
    #> │ str  ┆ u32       │
    #> ╞══════╪═══════════╡
    #> │ null ┆ 2         │
    #> │ a    ┆ 2         │
    #> │ null ┆ 2         │
    #> │ b    ┆ 2         │
    #> └──────┴───────────┘
