

# Get the last n elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2028)

## Description

Get the last n elements

## Usage

<pre><code class='language-R'>Expr_tail(n = 10)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_tail_:_n">n</code>
</td>
<td>
Number of elements to take.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = 1:11)$select(pl$col("x")$tail(3))
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ x   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 9   │
    #> │ 10  │
    #> │ 11  │
    #> └─────┘
