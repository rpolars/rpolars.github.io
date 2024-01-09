
# Get the first value.

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Get the first value.

## Usage

<pre><code class='language-R'>Expr_first
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
