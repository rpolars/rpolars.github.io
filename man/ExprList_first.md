
# First in sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__list.R#L202)

## Description

Get the first value of the sublists.

## Usage

<pre><code class='language-R'>ExprList_first()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(3:1, NULL, 1:2))) # NULL or integer() or list()
df$select(pl$col("a")$list$first())
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ a    │
    #> │ ---  │
    #> │ i32  │
    #> ╞══════╡
    #> │ 3    │
    #> │ null │
    #> │ 1    │
    #> └──────┘
