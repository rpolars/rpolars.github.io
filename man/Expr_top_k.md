

# Top k values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1491)

## Description

Return the <code>k</code> largest elements. This has time complexity:
<code class="reqn"> O(n + k \log{}n - ) </code>

## Usage

<pre><code class='language-R'>Expr_top_k(k)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_top_k_:_k">k</code>
</td>
<td>
Number of top values to get
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(6, 1, 0, NA, Inf, NaN))$select(pl$col("a")$top_k(5))
```

    #> shape: (5, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ NaN │
    #> │ inf │
    #> │ 6.0 │
    #> │ 1.0 │
    #> │ 0.0 │
    #> └─────┘
