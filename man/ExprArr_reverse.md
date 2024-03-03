

# Reverse values in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__array.R#L119)

## Description

Reverse values in an array

## Usage

<pre><code class='language-R'>ExprArr_reverse()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(c(1, 2), c(3, 4), c(NA_real_, 6)),
  schema = list(values = pl$Array(pl$Float64, 2))
)
df$with_columns(reverse = pl$col("values")$arr$reverse())
```

    #> shape: (3, 2)
    #> ┌───────────────┬───────────────┐
    #> │ values        ┆ reverse       │
    #> │ ---           ┆ ---           │
    #> │ array[f64, 2] ┆ array[f64, 2] │
    #> ╞═══════════════╪═══════════════╡
    #> │ [1.0, 2.0]    ┆ [2.0, 1.0]    │
    #> │ [3.0, 4.0]    ┆ [4.0, 3.0]    │
    #> │ [null, 6.0]   ┆ [6.0, null]   │
    #> └───────────────┴───────────────┘
