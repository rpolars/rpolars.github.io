
# Clip elements above maximum value

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2777)

## Description

Replace all values above a maximum value by this maximum value.

## Usage

<pre><code class='language-R'>Expr_clip_max(max)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_clip_max_:_max">max</code>
</td>
<td>
Maximum value, Expr returning a numeric.
</td>
</tr>
</table>

## Examples

``` r
library(polars)

pl$DataFrame(foo = c(-50L, 5L, NA_integer_, 50L))$
  with_columns(clipped = pl$col("foo")$clip_max(10))
```

    #> shape: (4, 2)
    #> ┌──────┬─────────┐
    #> │ foo  ┆ clipped │
    #> │ ---  ┆ ---     │
    #> │ i32  ┆ i32     │
    #> ╞══════╪═════════╡
    #> │ -50  ┆ -50     │
    #> │ 5    ┆ 5       │
    #> │ null ┆ null    │
    #> │ 50   ┆ 10      │
    #> └──────┴─────────┘
