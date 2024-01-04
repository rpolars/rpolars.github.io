
# Unique list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L106)

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
