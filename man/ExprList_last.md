
# Last in sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L214)

## Description

Get the last value of the sublists.

## Usage

<pre><code class='language-R'>ExprList_last()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(3:1, NULL, 1:2))) # NULL or integer() or list()
df$select(pl$col("a")$list$last())
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ a    │
    #> │ ---  │
    #> │ i32  │
    #> ╞══════╡
    #> │ 1    │
    #> │ null │
    #> │ 2    │
    #> └──────┘
