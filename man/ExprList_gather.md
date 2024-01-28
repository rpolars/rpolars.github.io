

# Get several values by index in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__list.R#L157)

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
<code id="ExprList_gather_:_index">index</code>
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
<code id="ExprList_gather_:_null_on_oob">null_on_oob</code>
</td>
<td>
Return a <code>null</code> value if index is out of bounds.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(c(3, 2, 1), 1, c(1, 2)))) #
idx = pl$Series(list(0:1, integer(), c(1L, 999L)))
df$select(pl$col("a")$list$gather(pl$lit(idx), null_on_oob = TRUE))
```

    #> shape: (3, 1)
    #> ┌─────────────┐
    #> │ a           │
    #> │ ---         │
    #> │ list[f64]   │
    #> ╞═════════════╡
    #> │ [3.0, 2.0]  │
    #> │ []          │
    #> │ [2.0, null] │
    #> └─────────────┘

``` r
# with implicit conversion to Expr
df$select(pl$col("a")$list$gather(list(0:1, integer(), c(1L, 999L)), null_on_oob = TRUE))
```

    #> shape: (3, 1)
    #> ┌─────────────┐
    #> │ a           │
    #> │ ---         │
    #> │ list[f64]   │
    #> ╞═════════════╡
    #> │ [3.0, 2.0]  │
    #> │ []          │
    #> │ [2.0, null] │
    #> └─────────────┘

``` r
# by some column name, must cast to an Int/Uint type to work
df$select(pl$col("a")$list$gather(pl$col("a")$cast(pl$List(pl$UInt64)), null_on_oob = TRUE))
```

    #> shape: (3, 1)
    #> ┌──────────────────┐
    #> │ a                │
    #> │ ---              │
    #> │ list[f64]        │
    #> ╞══════════════════╡
    #> │ [null, 1.0, 2.0] │
    #> │ [null]           │
    #> │ [2.0, null]      │
    #> └──────────────────┘
