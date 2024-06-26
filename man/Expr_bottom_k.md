

# Bottom k values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1412)

## Description

Return the <code>k</code> smallest elements. This has time complexity:
<code class="reqn"> O(n + k \log{}n - ) </code>

## Usage

<pre><code class='language-R'>Expr_bottom_k(k)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="k">k</code>
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

pl$DataFrame(a = c(6, 1, 0, NA, Inf, NaN))$select(pl$col("a")$bottom_k(5))
```

    #> shape: (5, 1)
    #> ┌──────┐
    #> │ a    │
    #> │ ---  │
    #> │ f64  │
    #> ╞══════╡
    #> │ null │
    #> │ 0.0  │
    #> │ 1.0  │
    #> │ 6.0  │
    #> │ inf  │
    #> └──────┘
