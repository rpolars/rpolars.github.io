

# Clip elements below minimum value

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2785)

## Description

Replace all values below a minimum value by this minimum value.

## Usage

<pre><code class='language-R'>Expr_clip_min(min)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_clip_min_:_min">min</code>
</td>
<td>
Minimum value, Expr returning a numeric.
</td>
</tr>
</table>

## Examples

``` r
library(polars)

pl$DataFrame(foo = c(-50L, 5L, NA_integer_, 50L))$
  with_columns(clipped = pl$col("foo")$clip_min(1))
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
    #> │ 50   ┆ 50      │
    #> └──────┴─────────┘
