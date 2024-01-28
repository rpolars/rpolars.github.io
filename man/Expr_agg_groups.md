

# Aggregate groups

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L20)

## Description

Get the group indexes of the group by operation. Should be used in
aggregation context only.

## Usage

<pre><code class='language-R'>Expr_agg_groups()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(
  group = c("one", "one", "one", "two", "two", "two"),
  value = c(94, 95, 96, 97, 97, 99)
))
df$group_by("group", maintain_order = TRUE)$agg(pl$col("value")$agg_groups())
```

    #> shape: (2, 2)
    #> ┌───────┬───────────┐
    #> │ group ┆ value     │
    #> │ ---   ┆ ---       │
    #> │ str   ┆ list[u32] │
    #> ╞═══════╪═══════════╡
    #> │ one   ┆ [0, 1, 2] │
    #> │ two   ┆ [3, 4, 5] │
    #> └───────┴───────────┘
