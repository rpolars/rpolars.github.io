

# Find the lower bound of a DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/after-wrappers.R#L20)

## Description

Find the lower bound of a DataType

## Usage

<pre><code class='language-R'>Expr_lower_bound()
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
