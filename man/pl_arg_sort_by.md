

# Return the row indices that would sort the columns

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/functions__lazy.R#L1264)

## Description

Return the row indices that would sort the columns

## Usage

<pre><code class='language-R'>pl_arg_sort_by(
  ...,
  descending = FALSE,
  nulls_last = FALSE,
  multithreaded = TRUE,
  maintain_order = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Column(s) to arg sort by. Can be Expr(s) or something coercible to
Expr(s). Strings are parsed as column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="descending">descending</code>
</td>
<td>
A logical. If <code>TRUE</code>, sort in descending order.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="nulls_last">nulls_last</code>
</td>
<td>
A logical. If <code>TRUE</code>, place <code>null</code> values last
insead of first.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="multithreaded">multithreaded</code>
</td>
<td>
A logical. If <code>TRUE</code>, sort using multiple threads.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="maintain_order">maintain_order</code>
</td>
<td>
Whether the order should be maintained if elements are equal. If
<code>TRUE</code>, streaming is not possible and performance might be
worse since this requires a stable search.
</td>
</tr>
</table>

## Value

Expr

## See Also

$arg_sort() to find the row indices that would sort an Expr.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(0, 1, 1, 0),
  b = c(3, 2, 3, 2)
)

df$with_columns(
  arg_sort_a = pl$arg_sort_by("a"),
  arg_sort_ab = pl$arg_sort_by(c("a", "b"), descending = TRUE)
)
```

    #> shape: (4, 4)
    #> ┌─────┬─────┬────────────┬─────────────┐
    #> │ a   ┆ b   ┆ arg_sort_a ┆ arg_sort_ab │
    #> │ --- ┆ --- ┆ ---        ┆ ---         │
    #> │ f64 ┆ f64 ┆ u32        ┆ u32         │
    #> ╞═════╪═════╪════════════╪═════════════╡
    #> │ 0.0 ┆ 3.0 ┆ 0          ┆ 2           │
    #> │ 1.0 ┆ 2.0 ┆ 3          ┆ 1           │
    #> │ 1.0 ┆ 3.0 ┆ 1          ┆ 0           │
    #> │ 0.0 ┆ 2.0 ┆ 2          ┆ 3           │
    #> └─────┴─────┴────────────┴─────────────┘

``` r
# we can also pass Expr
df$with_columns(
  arg_sort_a = pl$arg_sort_by(pl$col("a") * -1)
)
```

    #> shape: (4, 3)
    #> ┌─────┬─────┬────────────┐
    #> │ a   ┆ b   ┆ arg_sort_a │
    #> │ --- ┆ --- ┆ ---        │
    #> │ f64 ┆ f64 ┆ u32        │
    #> ╞═════╪═════╪════════════╡
    #> │ 0.0 ┆ 3.0 ┆ 1          │
    #> │ 1.0 ┆ 2.0 ┆ 2          │
    #> │ 1.0 ┆ 3.0 ┆ 0          │
    #> │ 0.0 ┆ 2.0 ┆ 3          │
    #> └─────┴─────┴────────────┘
