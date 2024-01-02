
# GroupBy First

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/group_by.R#L111)

## Description

Reduce the groups to the first value.

## Usage

<pre><code class='language-R'>GroupBy_first()
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
df$group_by("d", maintain_order = TRUE)$first()
```

    #> shape: (3, 4)
    #> ┌────────┬─────┬──────┬───────┐
    #> │ d      ┆ a   ┆ b    ┆ c     │
    #> │ ---    ┆ --- ┆ ---  ┆ ---   │
    #> │ str    ┆ f64 ┆ f64  ┆ bool  │
    #> ╞════════╪═════╪══════╪═══════╡
    #> │ Apple  ┆ 1.0 ┆ 0.5  ┆ true  │
    #> │ Orange ┆ 2.0 ┆ 0.5  ┆ true  │
    #> │ Banana ┆ 4.0 ┆ 13.0 ┆ false │
    #> └────────┴─────┴──────┴───────┘
