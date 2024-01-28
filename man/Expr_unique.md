

# Get unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__expr.R#L1843)

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
