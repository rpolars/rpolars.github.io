

# Get several values by index in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__list.R#L167)

## Description

This allows to extract several values per list. To extract a single
value by index, use <code>$list$get()</code>.

## Usage

<pre><code class='language-R'>ExprList_gather(index, null_on_oob = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="index">index</code>
</td>
<td>
An Expr or something coercible to an Expr, that can return several
single indices. Values are 0-indexed (so index 0 would return the first
item of every sublist) and negative values start from the end (index
<code>-1</code> returns the last item). If the index is out of bounds,
it will return a <code>null</code>. Strings are parsed as column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="null_on_oob">null_on_oob</code>
</td>
<td>
If <code>TRUE</code>, return <code>null</code> if an index is out of
bounds. Otherwise, raise an error.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = list(c(3, 2, 1), 1, c(1, 2)),
  idx = list(0:1, integer(), c(1L, 999L))
)
df$with_columns(
  gathered = pl$col("a")$list$gather("idx", null_on_oob = TRUE)
)
```

    #> shape: (3, 3)
    #> ┌─────────────────┬───────────┬─────────────┐
    #> │ a               ┆ idx       ┆ gathered    │
    #> │ ---             ┆ ---       ┆ ---         │
    #> │ list[f64]       ┆ list[i32] ┆ list[f64]   │
    #> ╞═════════════════╪═══════════╪═════════════╡
    #> │ [3.0, 2.0, 1.0] ┆ [0, 1]    ┆ [3.0, 2.0]  │
    #> │ [1.0]           ┆ []        ┆ []          │
    #> │ [1.0, 2.0]      ┆ [1, 999]  ┆ [2.0, null] │
    #> └─────────────────┴───────────┴─────────────┘

``` r
df$with_columns(
  gathered = pl$col("a")$list$gather(2, null_on_oob = TRUE)
)
```

    #> shape: (3, 3)
    #> ┌─────────────────┬───────────┬───────────┐
    #> │ a               ┆ idx       ┆ gathered  │
    #> │ ---             ┆ ---       ┆ ---       │
    #> │ list[f64]       ┆ list[i32] ┆ list[f64] │
    #> ╞═════════════════╪═══════════╪═══════════╡
    #> │ [3.0, 2.0, 1.0] ┆ [0, 1]    ┆ [1.0]     │
    #> │ [1.0]           ┆ []        ┆ [null]    │
    #> │ [1.0, 2.0]      ┆ [1, 999]  ┆ [null]    │
    #> └─────────────────┴───────────┴───────────┘

``` r
# by some column name, must cast to an Int/Uint type to work
df$with_columns(
  gathered = pl$col("a")$list$gather(pl$col("a")$cast(pl$List(pl$UInt64)), null_on_oob = TRUE)
)
```

    #> shape: (3, 3)
    #> ┌─────────────────┬───────────┬──────────────────┐
    #> │ a               ┆ idx       ┆ gathered         │
    #> │ ---             ┆ ---       ┆ ---              │
    #> │ list[f64]       ┆ list[i32] ┆ list[f64]        │
    #> ╞═════════════════╪═══════════╪══════════════════╡
    #> │ [3.0, 2.0, 1.0] ┆ [0, 1]    ┆ [null, 1.0, 2.0] │
    #> │ [1.0]           ┆ []        ┆ [null]           │
    #> │ [1.0, 2.0]      ┆ [1, 999]  ┆ [2.0, null]      │
    #> └─────────────────┴───────────┴──────────────────┘
