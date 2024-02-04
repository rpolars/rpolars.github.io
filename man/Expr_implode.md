

# Wrap column in list

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

## Description

Aggregate values into a list.

## Usage

<pre><code class='language-R'>Expr_implode()
</code></pre>

## Details

Use <code style="white-space: pre;">$to_struct()</code> to wrap a
DataFrame.

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = 1:3,
  b = 4:6
)
df$select(pl$all()$implode())
```

    #> shape: (1, 2)
    #> ┌───────────┬───────────┐
    #> │ a         ┆ b         │
    #> │ ---       ┆ ---       │
    #> │ list[i32] ┆ list[i32] │
    #> ╞═══════════╪═══════════╡
    #> │ [1, 2, 3] ┆ [4, 5, 6] │
    #> └───────────┴───────────┘
