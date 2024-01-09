
# Shift sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__list.R#L303)

## Description

Shift values by the given period.

## Usage

<pre><code class='language-R'>ExprList_shift(periods = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_shift_:_periods">periods</code>
</td>
<td>
Value. Number of places to shift (may be negative).
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
df$select(pl$col("s")$list$shift())
```

    #> shape: (2, 1)
    #> ┌────────────────┐
    #> │ s              │
    #> │ ---            │
    #> │ list[i32]      │
    #> ╞════════════════╡
    #> │ [null, 1, … 3] │
    #> │ [null, 10, 2]  │
    #> └────────────────┘
