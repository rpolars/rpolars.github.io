

# Get the first n elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__expr.R#L2044)

## Description

Get the first n elements

## Usage

<pre><code class='language-R'>Expr_head(n = 10)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_head_:_n">n</code>
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

pl$DataFrame(x = 1:11)$select(pl$col("x")$head(3))
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ x   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> └─────┘
