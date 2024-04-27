

# Mode

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

## Description

Compute the most occurring value(s). Can return multiple values if there
are ties.

## Usage

<pre><code class='language-R'>Expr_mode()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = 1:6, b = c(1L, 1L, 3L, 3L, 5L, 6L), c = c(1L, 1L, 2L, 2L, 3L, 3L))
df$select(pl$col("a")$mode())
```

    #> shape: (6, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 4   │
    #> │ 1   │
    #> │ 3   │
    #> │ 6   │
    #> │ 5   │
    #> │ 2   │
    #> └─────┘

``` r
df$select(pl$col("b")$mode())
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ b   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 3   │
    #> └─────┘

``` r
df$select(pl$col("c")$mode())
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ c   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 2   │
    #> │ 1   │
    #> │ 3   │
    #> └─────┘
