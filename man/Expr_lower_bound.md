
# Find the lower bound of a DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/#L)

## Description

Find the lower bound of a DataType

## Usage

<pre><code class='language-R'>Expr_lower_bound
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(
  x = 1:3, y = 1:3,
  schema = list(x = pl$UInt32, y = pl$Int32)
)$
  select(pl$all()$lower_bound())
```

    #> shape: (1, 2)
    #> ┌─────┬─────────────┐
    #> │ x   ┆ y           │
    #> │ --- ┆ ---         │
    #> │ u32 ┆ i32         │
    #> ╞═════╪═════════════╡
    #> │ 0   ┆ -2147483648 │
    #> └─────┴─────────────┘
