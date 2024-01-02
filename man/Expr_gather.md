
# Gather values by index

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__expr.R#L1582)

## Description

Gather values by index

## Usage

<pre><code class='language-R'>Expr_gather(indices)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gather_:_indices">indices</code>
</td>
<td>
R scalar/vector or Series, or Expr that leads to a Series of dtype
UInt32.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(1, 2, 4, 5, 8))$select(pl$col("a")$gather(c(0, 2, 4)))
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> │ 4.0 │
    #> │ 8.0 │
    #> └─────┘
