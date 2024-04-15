

# Reshape this Expr to a flat Series or a Series of Lists

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__expr.R#L2836)

## Description

Reshape this Expr to a flat Series or a Series of Lists

## Usage

<pre><code class='language-R'>Expr_reshape(dimensions)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_reshape_:_dimensions">dimensions</code>
</td>
<td>
A integer vector of length of the dimension size. If <code>-1</code> is
used in any of the dimensions, that dimension is inferred. Currently,
more than two dimensions not supported.
</td>
</tr>
</table>

## Value

Expr. If a single dimension is given, results in an expression of the
original data type. If a multiple dimensions are given, results in an
expression of data type List with shape equal to the dimensions.

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = 1:9)

df$select(pl$col("foo")$reshape(9))
```

    #> shape: (9, 1)
    #> ┌─────┐
    #> │ foo │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> │ 4   │
    #> │ 5   │
    #> │ 6   │
    #> │ 7   │
    #> │ 8   │
    #> │ 9   │
    #> └─────┘

``` r
df$select(pl$col("foo")$reshape(c(3, 3)))
```

    #> shape: (3, 1)
    #> ┌───────────┐
    #> │ foo       │
    #> │ ---       │
    #> │ list[i32] │
    #> ╞═══════════╡
    #> │ [1, 2, 3] │
    #> │ [4, 5, 6] │
    #> │ [7, 8, 9] │
    #> └───────────┘

``` r
# Use `-1` to infer the other dimension
df$select(pl$col("foo")$reshape(c(-1, 3)))
```

    #> shape: (3, 1)
    #> ┌───────────┐
    #> │ foo       │
    #> │ ---       │
    #> │ list[i32] │
    #> ╞═══════════╡
    #> │ [1, 2, 3] │
    #> │ [4, 5, 6] │
    #> │ [7, 8, 9] │
    #> └───────────┘

``` r
df$select(pl$col("foo")$reshape(c(3, -1)))
```

    #> shape: (3, 1)
    #> ┌───────────┐
    #> │ foo       │
    #> │ ---       │
    #> │ list[i32] │
    #> ╞═══════════╡
    #> │ [1, 2, 3] │
    #> │ [4, 5, 6] │
    #> │ [7, 8, 9] │
    #> └───────────┘
