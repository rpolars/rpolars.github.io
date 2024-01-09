
# Compute the square root of the elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__expr.R#L1055)

## Description

Compute the square root of the elements

## Usage

<pre><code class='language-R'>Expr_sqrt()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = -1:3)$with_columns(a_sqrt = pl$col("a")$sqrt())
```

    #> shape: (5, 2)
    #> ┌─────┬──────────┐
    #> │ a   ┆ a_sqrt   │
    #> │ --- ┆ ---      │
    #> │ i32 ┆ f64      │
    #> ╞═════╪══════════╡
    #> │ -1  ┆ NaN      │
    #> │ 0   ┆ 0.0      │
    #> │ 1   ┆ 1.0      │
    #> │ 2   ┆ 1.414214 │
    #> │ 3   ┆ 1.732051 │
    #> └─────┴──────────┘
