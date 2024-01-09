
# Aggregate groups

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Get the group indexes of the group by operation. Should be used in
aggregation context only.

## Usage

<pre><code class='language-R'>Expr_agg_groups
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
