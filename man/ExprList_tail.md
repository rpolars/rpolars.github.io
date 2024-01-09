
# Tails of sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__list.R#L356)

## Description

tail the first <code>n</code> values of every sublist.

## Usage

<pre><code class='language-R'>ExprList_tail(n = 5L)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_tail_:_n">n</code>
</td>
<td>
Numeric or Expr, number of values to return for each sublist.
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

df = pl$DataFrame(list(a = list(1:4, c(10L, 2L, 1L))))
df$select(pl$col("a")$list$tail(2))
```

    #> shape: (2, 1)
    #> ┌───────────┐
    #> │ a         │
    #> │ ---       │
    #> │ list[i32] │
    #> ╞═══════════╡
    #> │ [3, 4]    │
    #> │ [2, 1]    │
    #> └───────────┘
