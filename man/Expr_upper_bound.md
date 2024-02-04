

# Find the upper bound of a DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

## Description

Find the upper bound of a DataType

## Usage

<pre><code class='language-R'>Expr_upper_bound()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(
  x = c(1, 2, 3), y = -2:0,
  schema = list(x = pl$Float64, y = pl$Int32)
)$
  select(pl$all()$upper_bound())
```

    #> shape: (1, 2)
    #> ┌─────┬────────────┐
    #> │ x   ┆ y          │
    #> │ --- ┆ ---        │
    #> │ f64 ┆ i32        │
    #> ╞═════╪════════════╡
    #> │ inf ┆ 2147483647 │
    #> └─────┴────────────┘
