
# Unique list

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__list.R#L106)

## Description

Get the unique/distinct values in the list.

## Usage

<pre><code class='language-R'>ExprList_unique()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(1, 1, 2)))
df$select(pl$col("a")$list$unique())
```

    #> shape: (3, 1)
    #> ┌───────────┐
    #> │ a         │
    #> │ ---       │
    #> │ list[f64] │
    #> ╞═══════════╡
    #> │ [1.0]     │
    #> │ [1.0]     │
    #> │ [2.0]     │
    #> └───────────┘
