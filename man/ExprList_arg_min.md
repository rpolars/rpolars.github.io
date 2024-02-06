

# Get the index of the minimal value in list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L238)

## Description

Get the index of the minimal value in list

## Usage

<pre><code class='language-R'>ExprList_arg_min()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(s = list(1:2, 2:1)))
df$with_columns(
  arg_min = pl$col("s")$list$arg_min()
)
```

    #> shape: (2, 2)
    #> ┌───────────┬─────────┐
    #> │ s         ┆ arg_min │
    #> │ ---       ┆ ---     │
    #> │ list[i32] ┆ u32     │
    #> ╞═══════════╪═════════╡
    #> │ [1, 2]    ┆ 0       │
    #> │ [2, 1]    ┆ 1       │
    #> └───────────┴─────────┘
