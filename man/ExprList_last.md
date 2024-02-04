

# Get the last value in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__list.R#L183)

## Description

Get the last value in a list

## Usage

<pre><code class='language-R'>ExprList_last()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(3:1, NULL, 1:2)))
df$with_columns(
  last = pl$col("a")$list$last()
)
```

    #> shape: (3, 2)
    #> ┌───────────┬──────┐
    #> │ a         ┆ last │
    #> │ ---       ┆ ---  │
    #> │ list[i32] ┆ i32  │
    #> ╞═══════════╪══════╡
    #> │ [3, 2, 1] ┆ 1    │
    #> │ []        ┆ null │
    #> │ [1, 2]    ┆ 2    │
    #> └───────────┴──────┘
