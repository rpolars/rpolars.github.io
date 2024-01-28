

# Map alias of expression with an R function

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__name.R#L67)

## Description

Rename the output of an expression by mapping a function over the root
name.

## Usage

<pre><code class='language-R'>ExprName_map(fun)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprName_map_:_fun">fun</code>
</td>
<td>
an R function which takes a string as input and return a string
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(list(alice = 1:3))$select(
  pl$col("alice")$alias("joe_is_not_root")$name$map(\(x) paste0(x, "_and_bob"))
)
```

    #> shape: (3, 1)
    #> ┌───────────────┐
    #> │ alice_and_bob │
    #> │ ---           │
    #> │ i32           │
    #> ╞═══════════════╡
    #> │ 1             │
    #> │ 2             │
    #> │ 3             │
    #> └───────────────┘
