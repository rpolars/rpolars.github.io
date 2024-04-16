

# Get the first value in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__list.R#L202)

## Description

Get the first value in a list

## Usage

<pre><code class='language-R'>ExprList_first()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(3:1, NULL, 1:2)))
df$with_columns(
  first = pl$col("a")$list$first()
)
```

    #> shape: (3, 2)
    #> ┌───────────┬───────┐
    #> │ a         ┆ first │
    #> │ ---       ┆ ---   │
    #> │ list[i32] ┆ i32   │
    #> ╞═══════════╪═══════╡
    #> │ [3, 2, 1] ┆ 3     │
    #> │ []        ┆ null  │
    #> │ [1, 2]    ┆ 1     │
    #> └───────────┴───────┘
