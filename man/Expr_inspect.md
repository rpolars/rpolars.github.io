
# Inspect evaluated Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2246)

## Description

Print the value that this expression evaluates to and pass on the value.
The printing will happen when the expression evaluates, not when it is
formed.

## Usage

<pre><code class='language-R'>Expr_inspect(fmt = "{}")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_inspect_:_fmt">fmt</code>
</td>
<td>
format string, should contain one set of <code>{}</code> where object
will be printed. This formatting mimics python "string".format() use in
py-polars.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$select(pl$lit(1:5)$inspect(
  "Here's what the Series looked like before keeping the first two values: {}"
)$head(2))
```

    #> Here's what the Series looked like before keeping the first two values: shape: (5,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #>  5
    #> ]

    #> shape: (2, 1)
    #> ┌─────┐
    #> │     │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> └─────┘
