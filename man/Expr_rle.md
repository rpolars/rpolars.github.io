

# Get the lengths of runs of identical values

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__expr.R#L3402)

## Description

Get the lengths of runs of identical values

## Usage

<pre><code class='language-R'>Expr_rle()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(s = c(1, 1, 2, 1, NA, 1, 3, 3))
df$select(pl$col("s")$rle())$unnest("s")
```

    #> shape: (6, 2)
    #> ┌─────────┬────────┐
    #> │ lengths ┆ values │
    #> │ ---     ┆ ---    │
    #> │ i32     ┆ f64    │
    #> ╞═════════╪════════╡
    #> │ 2       ┆ 1.0    │
    #> │ 1       ┆ 2.0    │
    #> │ 1       ┆ 1.0    │
    #> │ 1       ┆ null   │
    #> │ 1       ┆ 1.0    │
    #> │ 2       ┆ 3.0    │
    #> └─────────┴────────┘
