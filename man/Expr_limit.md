

# Get the first n elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__expr.R#L2048)

## Description

This is an alias for
<code style="white-space: pre;">\<Expr\>$head()</code>.

## Usage

<pre><code class='language-R'>Expr_limit(n = 10)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_limit_:_n">n</code>
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

pl$DataFrame(x = 1:11)$select(pl$col("x")$limit(3))
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
