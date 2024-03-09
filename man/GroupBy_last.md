

# GroupBy Last

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/group_by.R#L148)

## Description

Reduce the groups to the last value.

## Usage

<pre><code class='language-R'>GroupBy_last()
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
df$group_by("d", maintain_order = TRUE)$last()
```

    #> shape: (3, 4)
    #> ┌────────┬─────┬──────┬───────┐
    #> │ d      ┆ a   ┆ b    ┆ c     │
    #> │ ---    ┆ --- ┆ ---  ┆ ---   │
    #> │ str    ┆ f64 ┆ f64  ┆ bool  │
    #> ╞════════╪═════╪══════╪═══════╡
    #> │ Apple  ┆ 3.0 ┆ 10.0 ┆ false │
    #> │ Orange ┆ 2.0 ┆ 0.5  ┆ true  │
    #> │ Banana ┆ 5.0 ┆ 14.0 ┆ true  │
    #> └────────┴─────┴──────┴───────┘
