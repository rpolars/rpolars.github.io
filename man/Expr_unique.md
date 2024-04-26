

# Get unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1794)

## Description

Get unique values

## Usage

<pre><code class='language-R'>Expr_unique(maintain_order = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="maintain_order">maintain_order</code>
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
