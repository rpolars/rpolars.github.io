

# Clip elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/expr__expr.R#L2669)

## Description

Clip (limit) the values in an array to a <code>min</code> and
<code>max</code> boundary. This only works for numerical types.

## Usage

<pre><code class='language-R'>Expr_clip(min, max)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_clip_:_min">min</code>
</td>
<td>
Minimum value, Expr returning a numeric.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_clip_:_max">max</code>
</td>
<td>
Maximum value, Expr returning a numeric.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(foo = c(-50L, 5L, NA_integer_, 50L))$
  with_columns(clipped = pl$col("foo")$clip(1, 10))
```

    #> shape: (4, 2)
    #> ┌──────┬─────────┐
    #> │ foo  ┆ clipped │
    #> │ ---  ┆ ---     │
    #> │ i32  ┆ i32     │
    #> ╞══════╪═════════╡
    #> │ -50  ┆ 1       │
    #> │ 5    ┆ 5       │
    #> │ null ┆ null    │
    #> │ 50   ┆ 10      │
    #> └──────┴─────────┘
