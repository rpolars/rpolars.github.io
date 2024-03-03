

# Compute difference between list values

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__list.R#L298)

## Description

This computes the first discrete difference between shifted items of
every list. The parameter <code>n</code> gives the interval between
items to subtract, e.g <code>n = 2</code> the output will be the
difference between the 1st and the 3rd value, the 2nd and 4th value,
etc.

## Usage

<pre><code class='language-R'>ExprList_diff(n = 1, null_behavior = c("ignore", "drop"))
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_diff_:_n">n</code>
</td>
<td>
Number of slots to shift. If negative, then it starts from the end.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_diff_:_null_behavior">null_behavior</code>
</td>
<td>
How to handle <code>null</code> values. Either <code>“ignore”</code>
(default) or <code>“drop”</code>.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(s = list(1:4, c(10L, 2L, 1L))))
df$with_columns(diff = pl$col("s")$list$diff(2))
```

    #> shape: (2, 2)
    #> ┌─────────────┬───────────────────┐
    #> │ s           ┆ diff              │
    #> │ ---         ┆ ---               │
    #> │ list[i32]   ┆ list[i32]         │
    #> ╞═════════════╪═══════════════════╡
    #> │ [1, 2, … 4] ┆ [null, null, … 2] │
    #> │ [10, 2, 1]  ┆ [null, null, -9]  │
    #> └─────────────┴───────────────────┘

``` r
# negative value starts shifting from the end
df$with_columns(diff = pl$col("s")$list$diff(-2))
```

    #> shape: (2, 2)
    #> ┌─────────────┬──────────────────┐
    #> │ s           ┆ diff             │
    #> │ ---         ┆ ---              │
    #> │ list[i32]   ┆ list[i32]        │
    #> ╞═════════════╪══════════════════╡
    #> │ [1, 2, … 4] ┆ [-2, -2, … null] │
    #> │ [10, 2, 1]  ┆ [9, null, null]  │
    #> └─────────────┴──────────────────┘
