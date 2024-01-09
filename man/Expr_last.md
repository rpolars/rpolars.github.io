
# Get the last value

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Get the last value

## Usage

<pre><code class='language-R'>Expr_last
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = 3:1)$with_columns(last = pl$col("x")$last())
```

    #> shape: (3, 2)
    #> ┌─────┬──────┐
    #> │ x   ┆ last │
    #> │ --- ┆ ---  │
    #> │ i32 ┆ i32  │
    #> ╞═════╪══════╡
    #> │ 3   ┆ 1    │
    #> │ 2   ┆ 1    │
    #> │ 1   ┆ 1    │
    #> └─────┴──────┘
