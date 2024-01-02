
# Mean of lists

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__list.R#L73)

## Description

Compute the mean value of the lists in the array.

## Usage

<pre><code class='language-R'>ExprList_mean()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(values = pl$Series(list(1L, 2:3)))
df$select(pl$col("values")$list$mean())
```

    #> shape: (2, 1)
    #> ┌────────┐
    #> │ values │
    #> │ ---    │
    #> │ f64    │
    #> ╞════════╡
    #> │ 1.0    │
    #> │ 2.5    │
    #> └────────┘
