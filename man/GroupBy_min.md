

# GroupBy Min

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/group_by.R#L212)

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
