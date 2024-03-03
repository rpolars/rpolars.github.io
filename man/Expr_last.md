

# Get the last value

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/after-wrappers.R#L20)

## Description

Get the last value

## Usage

<pre><code class='language-R'>Expr_last()
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
