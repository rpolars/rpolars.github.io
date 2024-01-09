
# Lengths arrays in list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L21)

## Description

Get the length of the arrays as UInt32

## Usage

<pre><code class='language-R'>ExprList_lengths()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list_of_strs = pl$Series(list(c("a", "b"), "c")))
df$with_columns(pl$col("list_of_strs")$list$lengths()$alias("list_of_strs_lengths"))
```

    #> shape: (2, 2)
    #> ┌──────────────┬──────────────────────┐
    #> │ list_of_strs ┆ list_of_strs_lengths │
    #> │ ---          ┆ ---                  │
    #> │ list[str]    ┆ u32                  │
    #> ╞══════════════╪══════════════════════╡
    #> │ ["a", "b"]   ┆ 2                    │
    #> │ ["c"]        ┆ 1                    │
    #> └──────────────┴──────────────────────┘
