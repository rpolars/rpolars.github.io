

# Approx count unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

This is done using the HyperLogLog++ algorithm for cardinality
estimation.

## Usage

<pre><code class='language-R'>Expr_approx_n_unique()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(iris[, 4:5])$
  with_columns(count = pl$col("Species")$approx_n_unique())
```

    #> shape: (150, 3)
    #> ┌─────────────┬───────────┬───────┐
    #> │ Petal.Width ┆ Species   ┆ count │
    #> │ ---         ┆ ---       ┆ ---   │
    #> │ f64         ┆ cat       ┆ u32   │
    #> ╞═════════════╪═══════════╪═══════╡
    #> │ 0.2         ┆ setosa    ┆ 3     │
    #> │ 0.2         ┆ setosa    ┆ 3     │
    #> │ 0.2         ┆ setosa    ┆ 3     │
    #> │ 0.2         ┆ setosa    ┆ 3     │
    #> │ 0.2         ┆ setosa    ┆ 3     │
    #> │ …           ┆ …         ┆ …     │
    #> │ 2.3         ┆ virginica ┆ 3     │
    #> │ 1.9         ┆ virginica ┆ 3     │
    #> │ 2.0         ┆ virginica ┆ 3     │
    #> │ 2.3         ┆ virginica ┆ 3     │
    #> │ 1.8         ┆ virginica ┆ 3     │
    #> └─────────────┴───────────┴───────┘
