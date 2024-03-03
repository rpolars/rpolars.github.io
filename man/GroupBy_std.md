

# GroupBy Std

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/group_by.R#L260)

## Description

Reduce the groups to the standard deviation value.

## Usage

<pre><code class='language-R'>GroupBy_std()
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
df$group_by("d", maintain_order = TRUE)$std()
```

    #> shape: (3, 4)
    #> ┌────────┬──────────┬──────────┬──────────┐
    #> │ d      ┆ a        ┆ b        ┆ c        │
    #> │ ---    ┆ ---      ┆ ---      ┆ ---      │
    #> │ str    ┆ f64      ┆ f64      ┆ f64      │
    #> ╞════════╪══════════╪══════════╪══════════╡
    #> │ Apple  ┆ 1.0      ┆ 4.804512 ┆ 0.57735  │
    #> │ Orange ┆ null     ┆ null     ┆ null     │
    #> │ Banana ┆ 0.707107 ┆ 0.707107 ┆ 0.707107 │
    #> └────────┴──────────┴──────────┴──────────┘
