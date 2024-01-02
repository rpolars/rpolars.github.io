
# GroupBy Mean

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/group_by.R#L159)

## Description

Reduce the groups to the mean value.

## Usage

<pre><code class='language-R'>GroupBy_mean()
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
df$group_by("d", maintain_order = TRUE)$mean()
```

    #> shape: (3, 4)
    #> ┌────────┬─────┬──────────┬──────────┐
    #> │ d      ┆ a   ┆ b        ┆ c        │
    #> │ ---    ┆ --- ┆ ---      ┆ ---      │
    #> │ str    ┆ f64 ┆ f64      ┆ f64      │
    #> ╞════════╪═════╪══════════╪══════════╡
    #> │ Apple  ┆ 2.0 ┆ 4.833333 ┆ 0.666667 │
    #> │ Orange ┆ 2.0 ┆ 0.5      ┆ 1.0      │
    #> │ Banana ┆ 4.5 ┆ 13.5     ┆ 0.5      │
    #> └────────┴─────┴──────────┴──────────┘
