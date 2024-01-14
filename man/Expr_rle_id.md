
# Map values to run IDs

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3665)

## Description

Similar to $rle(), but it maps each value to an ID corresponding to the
run into which it falls. This is especially useful when you want to
define groups by runs of identical values rather than the values
themselves. Note that the ID is 0-indexed.

## Usage

<pre><code class='language-R'>Expr_rle_id()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c(1, 2, 1, 1, 1, 4))
df$with_columns(a_r = pl$col("a")$rle_id())
```

    #> shape: (6, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ a_r │
    #> │ --- ┆ --- │
    #> │ f64 ┆ u32 │
    #> ╞═════╪═════╡
    #> │ 1.0 ┆ 0   │
    #> │ 2.0 ┆ 1   │
    #> │ 1.0 ┆ 2   │
    #> │ 1.0 ┆ 2   │
    #> │ 1.0 ┆ 2   │
    #> │ 4.0 ┆ 3   │
    #> └─────┴─────┘
