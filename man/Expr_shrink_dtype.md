

# Shrink numeric columns to the minimal required datatype

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/after-wrappers.R#L20)

## Description

Shrink to the dtype needed to fit the extrema of this Series. This can
be used to reduce memory pressure.

## Usage

<pre><code class='language-R'>Expr_shrink_dtype()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = 1:3,
  b = c(1, 2, 3)
)
df
```

    #> shape: (3, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ f64 │
    #> ╞═════╪═════╡
    #> │ 1   ┆ 1.0 │
    #> │ 2   ┆ 2.0 │
    #> │ 3   ┆ 3.0 │
    #> └─────┴─────┘

``` r
df$with_columns(pl$all()$shrink_dtype()$name$suffix("_shrunk"))
```

    #> shape: (3, 4)
    #> ┌─────┬─────┬──────────┬──────────┐
    #> │ a   ┆ b   ┆ a_shrunk ┆ b_shrunk │
    #> │ --- ┆ --- ┆ ---      ┆ ---      │
    #> │ i32 ┆ f64 ┆ i8       ┆ f32      │
    #> ╞═════╪═════╪══════════╪══════════╡
    #> │ 1   ┆ 1.0 ┆ 1        ┆ 1.0      │
    #> │ 2   ┆ 2.0 ┆ 2        ┆ 2.0      │
    #> │ 3   ┆ 3.0 ┆ 3        ┆ 3.0      │
    #> └─────┴─────┴──────────┴──────────┘
