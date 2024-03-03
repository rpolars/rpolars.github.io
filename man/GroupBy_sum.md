

# GroupBy Sum

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/group_by.R#L228)

## Description

Reduce the groups to the sum value.

## Usage

<pre><code class='language-R'>GroupBy_sum()
</code></pre>

## Value

aggregated DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1, 2, 2, 3, 4, 5),
  b = c(0.5, 0.5, 4, 10, 13, 14),
  c = c(TRUE, TRUE, TRUE, FALSE, FALSE, TRUE),
  d = c("Apple", "Orange", "Apple", "Apple", "Banana", "Banana")
)
df$group_by("d", maintain_order = TRUE)$sum()
```

    #> shape: (3, 4)
    #> ┌────────┬─────┬──────┬─────┐
    #> │ d      ┆ a   ┆ b    ┆ c   │
    #> │ ---    ┆ --- ┆ ---  ┆ --- │
    #> │ str    ┆ f64 ┆ f64  ┆ u32 │
    #> ╞════════╪═════╪══════╪═════╡
    #> │ Apple  ┆ 6.0 ┆ 14.5 ┆ 2   │
    #> │ Orange ┆ 2.0 ┆ 0.5  ┆ 1   │
    #> │ Banana ┆ 9.0 ┆ 27.0 ┆ 1   │
    #> └────────┴─────┴──────┴─────┘
