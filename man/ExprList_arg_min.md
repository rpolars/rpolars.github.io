
# Arg min sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__list.R#L258)

## Description

Retrieve the index of the minimal value in every sublist.

## Usage

<pre><code class='language-R'>ExprList_arg_min()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(s = list(1:2, 2:1)))
df$select(pl$col("s")$list$arg_min())
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ s   │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 0   │
    #> │ 1   │
    #> └─────┘
