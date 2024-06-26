

# Gather values by index

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1538)

## Description

Gather values by index

## Usage

<pre><code class='language-R'>Expr_gather(indices)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="indices">indices</code>
</td>
<td>
R vector or Series, or Expr that leads to a Series of dtype Int64.
(0-indexed)
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = 1:10)

df$select(pl$col("a")$gather(c(0, 2, 4, -1)))
```

    #> shape: (4, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 3   │
    #> │ 5   │
    #> │ 10  │
    #> └─────┘
