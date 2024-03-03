

# Get the index of the minimal value in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__array.R#L222)

## Description

Get the index of the minimal value in an array

## Usage

<pre><code class='language-R'>ExprArr_arg_min()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(1:2, 2:1),
  schema = list(values = pl$Array(pl$Int32, 2))
)
df$with_columns(
  arg_min = pl$col("values")$arr$arg_min()
)
```

    #> shape: (2, 2)
    #> ┌───────────────┬─────────┐
    #> │ values        ┆ arg_min │
    #> │ ---           ┆ ---     │
    #> │ array[i32, 2] ┆ u32     │
    #> ╞═══════════════╪═════════╡
    #> │ [1, 2]        ┆ 0       │
    #> │ [2, 1]        ┆ 1       │
    #> └───────────────┴─────────┘
