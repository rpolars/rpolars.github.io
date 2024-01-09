
# Count missing values

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Count missing values

## Usage

<pre><code class='language-R'>Expr_null_count
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
