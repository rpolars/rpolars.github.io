

# Get the index of the maximal value in list

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__list.R#L247)

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
