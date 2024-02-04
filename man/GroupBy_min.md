

# GroupBy Min

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/group_by.R#L192)

## Description

Reduce the groups to the minimum value.

## Usage

<pre><code class='language-R'>GroupBy_min()
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
df$group_by("d", maintain_order = TRUE)$min()
```

    #> shape: (3, 4)
    #> ┌────────┬─────┬──────┬───────┐
    #> │ d      ┆ a   ┆ b    ┆ c     │
    #> │ ---    ┆ --- ┆ ---  ┆ ---   │
    #> │ str    ┆ f64 ┆ f64  ┆ bool  │
    #> ╞════════╪═════╪══════╪═══════╡
    #> │ Apple  ┆ 1.0 ┆ 0.5  ┆ false │
    #> │ Orange ┆ 2.0 ┆ 0.5  ┆ true  │
    #> │ Banana ┆ 4.0 ┆ 13.0 ┆ false │
    #> └────────┴─────┴──────┴───────┘
