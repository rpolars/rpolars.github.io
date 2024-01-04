
# Heads of sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/expr__list.R#L341)

## Description

head the first <code>n</code> values of every sublist.

## Usage

<pre><code class='language-R'>ExprList_head(n = 5L)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_head_:_n">n</code>
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
df$select(pl$col("a")$list$head(2))
```

    #> shape: (2, 1)
    #> ┌───────────┐
    #> │ a         │
    #> │ ---       │
    #> │ list[i32] │
    #> ╞═══════════╡
    #> │ [1, 2]    │
    #> │ [10, 2]   │
    #> └───────────┘
