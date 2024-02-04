

# Get the first value.

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

## Description

Get the first value.

## Usage

<pre><code class='language-R'>Expr_first()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = 3:1)$with_columns(first = pl$col("x")$first())
```

    #> shape: (3, 2)
    #> ┌─────┬───────┐
    #> │ x   ┆ first │
    #> │ --- ┆ ---   │
    #> │ i32 ┆ i32   │
    #> ╞═════╪═══════╡
    #> │ 3   ┆ 3     │
    #> │ 2   ┆ 3     │
    #> │ 1   ┆ 3     │
    #> └─────┴───────┘
