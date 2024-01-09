
# Slice sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__list.R#L319)

## Description

Slice every sublist.

## Usage

<pre><code class='language-R'>ExprList_slice(offset, length = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_slice_:_offset">offset</code>
</td>
<td>
value or Expr. Start index. Negative indexing is supported.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_slice_:_length">length</code>
</td>
<td>
value or Expr. Length of the slice. If set to <code>None</code>
(default), the slice is taken to the end of the list.
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

df = pl$DataFrame(list(s = list(1:4, c(10L, 2L, 1L))))
df$select(pl$col("s")$list$slice(2))
```

    #> shape: (2, 1)
    #> ┌───────────┐
    #> │ s         │
    #> │ ---       │
    #> │ list[i32] │
    #> ╞═══════════╡
    #> │ [3, 4]    │
    #> │ [1]       │
    #> └───────────┘
