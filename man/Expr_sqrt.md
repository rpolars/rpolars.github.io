

# Compute the square root of the elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__expr.R#L1035)

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
