

# GroupBy Var

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/group_by.R#L242)

## Description

Reduce the groups to the variance value.

## Usage

<pre><code class='language-R'>GroupBy_var()
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
df$group_by("d", maintain_order = TRUE)$var()
```

    #> shape: (3, 4)
    #> ┌────────┬──────┬───────────┬──────────┐
    #> │ d      ┆ a    ┆ b         ┆ c        │
    #> │ ---    ┆ ---  ┆ ---       ┆ ---      │
    #> │ str    ┆ f64  ┆ f64       ┆ f64      │
    #> ╞════════╪══════╪═══════════╪══════════╡
    #> │ Apple  ┆ 1.0  ┆ 23.083333 ┆ 0.333333 │
    #> │ Orange ┆ null ┆ null      ┆ null     │
    #> │ Banana ┆ 0.5  ┆ 0.5       ┆ 0.5      │
    #> └────────┴──────┴───────────┴──────────┘
