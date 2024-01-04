
# Diff sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/expr__list.R#L287)

## Description

Calculate the n-th discrete difference of every sublist.

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
Number of slots to shift
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_diff_:_null_behavior">null_behavior</code>
</td>
<td>
choice "ignore"(default) "drop"
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
df$select(pl$col("s")$list$diff(1))
```

    #> shape: (2, 1)
    #> ┌────────────────┐
    #> │ s              │
    #> │ ---            │
    #> │ list[i32]      │
    #> ╞════════════════╡
    #> │ [null, 1, … 1] │
    #> │ [null, -8, -1] │
    #> └────────────────┘
