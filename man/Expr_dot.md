

# Dot product

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1357)

## Description

Compute the dot/inner product between two Expressions.

## Usage

<pre><code class='language-R'>Expr_dot(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="other">other</code>
</td>
<td>
numeric or string value; accepts expression input.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(
  a = 1:4, b = c(1, 2, 3, 4)
)$with_columns(
  pl$col("a")$dot(pl$col("b"))$alias("a dot b"),
  pl$col("a")$dot(pl$col("a"))$alias("a dot a")
)
```

    #> shape: (4, 4)
    #> ┌─────┬─────┬─────────┬─────────┐
    #> │ a   ┆ b   ┆ a dot b ┆ a dot a │
    #> │ --- ┆ --- ┆ ---     ┆ ---     │
    #> │ i32 ┆ f64 ┆ f64     ┆ i32     │
    #> ╞═════╪═════╪═════════╪═════════╡
    #> │ 1   ┆ 1.0 ┆ 30.0    ┆ 30      │
    #> │ 2   ┆ 2.0 ┆ 30.0    ┆ 30      │
    #> │ 3   ┆ 3.0 ┆ 30.0    ┆ 30      │
    #> │ 4   ┆ 4.0 ┆ 30.0    ┆ 30      │
    #> └─────┴─────┴─────────┴─────────┘
