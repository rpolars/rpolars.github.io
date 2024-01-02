
# Join sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__list.R#L243)

## Description

Join all string items in a sublist and place a separator between them.
This errors if inner type of list <code style="white-space: pre;">!=
Utf8</code>.

## Usage

<pre><code class='language-R'>ExprList_join(separator)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_join_:_separator">separator</code>
</td>
<td>
String to separate the items with. Can be an Expr.
</td>
</tr>
</table>

## Format

function

## Value

Series of dtype Utf8

## Examples

``` r
library(polars)

df = pl$DataFrame(list(s = list(c("a", "b", "c"), c("x", "y"))))
df$select(pl$col("s")$list$join(" "))
```

    #> shape: (2, 1)
    #> ┌───────┐
    #> │ s     │
    #> │ ---   │
    #> │ str   │
    #> ╞═══════╡
    #> │ a b c │
    #> │ x y   │
    #> └───────┘
