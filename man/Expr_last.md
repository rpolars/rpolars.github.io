

# Get the last value

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

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
