

# Gather every nth element in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__list.R#L185)

## Description

Gather every nth element in a list

## Usage

<pre><code class='language-R'>ExprList_gather_every(n, offset = 0)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_gather_every_:_n">n</code>
</td>
<td>
Positive integer.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_gather_every_:_offset">offset</code>
</td>
<td>
Starting index.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = list(1:5, 6:8, 9:12),
  n = c(2, 1, 3),
  offset = c(0, 1, 0)
)

df$with_columns(
  gather_every = pl$col("a")$list$gather_every(pl$col("n"), offset = pl$col("offset"))
)
```

    #> shape: (3, 4)
    #> ┌───────────────┬─────┬────────┬──────────────┐
    #> │ a             ┆ n   ┆ offset ┆ gather_every │
    #> │ ---           ┆ --- ┆ ---    ┆ ---          │
    #> │ list[i32]     ┆ f64 ┆ f64    ┆ list[i32]    │
    #> ╞═══════════════╪═════╪════════╪══════════════╡
    #> │ [1, 2, … 5]   ┆ 2.0 ┆ 0.0    ┆ [1, 3, 5]    │
    #> │ [6, 7, 8]     ┆ 1.0 ┆ 1.0    ┆ [7, 8]       │
    #> │ [9, 10, … 12] ┆ 3.0 ┆ 0.0    ┆ [9, 12]      │
    #> └───────────────┴─────┴────────┴──────────────┘
