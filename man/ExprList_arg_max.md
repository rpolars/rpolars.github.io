

# Get the index of the maximal value in list

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__list.R#L243)

## Description

Get the index of the maximal value in list

## Usage

<pre><code class='language-R'>ExprList_arg_max()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(s = list(1:2, 2:1)))
df$with_columns(
  arg_max = pl$col("s")$list$arg_max()
)
```

    #> shape: (2, 2)
    #> ┌───────────┬─────────┐
    #> │ s         ┆ arg_max │
    #> │ ---       ┆ ---     │
    #> │ list[i32] ┆ u32     │
    #> ╞═══════════╪═════════╡
    #> │ [1, 2]    ┆ 1       │
    #> │ [2, 1]    ┆ 0       │
    #> └───────────┴─────────┘
