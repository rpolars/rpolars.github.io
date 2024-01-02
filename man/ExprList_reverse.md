
# Reverse list

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__list.R#L93)

## Description

Reverse the arrays in the list.

## Usage

<pre><code class='language-R'>ExprList_reverse()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(
  values = list(3:1, c(9L, 1:2))
))
df$select(pl$col("values")$list$reverse())
```

    #> shape: (2, 1)
    #> ┌───────────┐
    #> │ values    │
    #> │ ---       │
    #> │ list[i32] │
    #> ╞═══════════╡
    #> │ [1, 2, 3] │
    #> │ [2, 1, 9] │
    #> └───────────┘
