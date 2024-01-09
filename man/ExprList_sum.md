
# Sum lists

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__list.R#L34)

## Description

Sum all the lists in the array.

## Usage

<pre><code class='language-R'>ExprList_sum()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(values = pl$Series(list(1L, 2:3)))
df$select(pl$col("values")$list$sum())
```

    #> shape: (2, 1)
    #> ┌────────┐
    #> │ values │
    #> │ ---    │
    #> │ i32    │
    #> ╞════════╡
    #> │ 1      │
    #> │ 5      │
    #> └────────┘
