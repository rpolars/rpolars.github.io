
# Sublists contains

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L227)

## Description

Check if sublists contain the given item.

## Usage

<pre><code class='language-R'>ExprList_contains(item)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_contains_:_item">item</code>
</td>
<td>
any into Expr/literal
</td>
</tr>
</table>

## Format

function

## Value

Expr of a boolean mask

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(3:1, NULL, 1:2))) # NULL or integer() or list()
df$select(pl$col("a")$list$contains(1L))
```

    #> shape: (3, 1)
    #> ┌───────┐
    #> │ a     │
    #> │ ---   │
    #> │ bool  │
    #> ╞═══════╡
    #> │ true  │
    #> │ false │
    #> │ true  │
    #> └───────┘
