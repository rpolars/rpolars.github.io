
# #’ Min lists

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L60)

## Description

Compute the min value of the lists in the array.

## Usage

<pre><code class='language-R'>ExprList_min()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(values = pl$Series(list(1L, 2:3)))
df$select(pl$col("values")$list$min())
```

    #> shape: (2, 1)
    #> ┌────────┐
    #> │ values │
    #> │ ---    │
    #> │ i32    │
    #> ╞════════╡
    #> │ 1      │
    #> │ 2      │
    #> └────────┘
