
# take in sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/expr__list.R#L186)

## Description

Get the take value of the sublists.

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
R list of integers for each sub-element or Expr or Series of type
<code>List\[usize\]</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_gather_:_null_on_oob">null_on_oob</code>
</td>
<td>
boolean
</td>
</tr>
</table>

## Format

function

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
