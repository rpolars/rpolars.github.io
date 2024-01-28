

# Find the upper bound of a DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L20)

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
