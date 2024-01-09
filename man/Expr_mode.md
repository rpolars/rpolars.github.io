
# Mode

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Compute the most occurring value(s). Can return multiple values if there
are ties.

## Usage

<pre><code class='language-R'>Expr_mode
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
    #> │ 3   │
    #> │ 6   │
    #> │ 1   │
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
    #> │ 3   │
    #> │ 1   │
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
    #> │ 3   │
    #> │ 1   │
    #> │ 2   │
    #> └─────┘
