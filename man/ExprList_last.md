

# Get the last value in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__list.R#L183)

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
