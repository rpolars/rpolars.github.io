

# GroupBy Median

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/group_by.R#L176)

## Description

Reduce the groups to the median value.

## Usage

<pre><code class='language-R'>GroupBy_median()
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
df$group_by("d", maintain_order = TRUE)$median()
```

    #> shape: (3, 4)
    #> ┌────────┬─────┬──────┬──────┐
    #> │ d      ┆ a   ┆ b    ┆ c    │
    #> │ ---    ┆ --- ┆ ---  ┆ ---  │
    #> │ str    ┆ f64 ┆ f64  ┆ bool │
    #> ╞════════╪═════╪══════╪══════╡
    #> │ Apple  ┆ 2.0 ┆ 4.0  ┆ null │
    #> │ Orange ┆ 2.0 ┆ 0.5  ┆ null │
    #> │ Banana ┆ 4.5 ┆ 13.5 ┆ null │
    #> └────────┴─────┴──────┴──────┘
