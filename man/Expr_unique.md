

# Get unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__expr.R#L1849)

## Description

Get unique values

## Usage

<pre><code class='language-R'>Expr_unique(maintain_order = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_unique_:_maintain_order">maintain_order</code>
</td>
<td>
If <code>TRUE</code>, the unique values are returned in order of
appearance.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(iris)$select(pl$col("Species")$unique())
```

    #> shape: (3, 1)
    #> ┌────────────┐
    #> │ Species    │
    #> │ ---        │
    #> │ cat        │
    #> ╞════════════╡
    #> │ setosa     │
    #> │ versicolor │
    #> │ virginica  │
    #> └────────────┘
