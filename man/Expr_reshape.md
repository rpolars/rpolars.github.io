
# Reshape

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2900)

## Description

Reshape an Expr to a flat Series or a Series of Lists.

## Usage

<pre><code class='language-R'>Expr_reshape(dims)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_reshape_:_dims">dims</code>
</td>
<td>
Numeric vec of the dimension sizes. If a -1 is used in any of the
dimensions, that dimension is inferred.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$select(pl$lit(1:12)$reshape(c(3, 4)))
```

    #> shape: (3, 1)
    #> ┌───────────────┐
    #> │               │
    #> │ ---           │
    #> │ list[i32]     │
    #> ╞═══════════════╡
    #> │ [1, 2, … 4]   │
    #> │ [5, 6, … 8]   │
    #> │ [9, 10, … 12] │
    #> └───────────────┘

``` r
pl$select(pl$lit(1:12)$reshape(c(3, -1)))
```

    #> shape: (3, 1)
    #> ┌───────────────┐
    #> │               │
    #> │ ---           │
    #> │ list[i32]     │
    #> ╞═══════════════╡
    #> │ [1, 2, … 4]   │
    #> │ [5, 6, … 8]   │
    #> │ [9, 10, … 12] │
    #> └───────────────┘
