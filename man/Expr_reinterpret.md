

# Reinterpret bits

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2386)

## Description

Reinterpret the underlying bits as a signed/unsigned integer. This
operation is only allowed for Int64. For lower bits integers, you can
safely use the cast operation.

## Usage

<pre><code class='language-R'>Expr_reinterpret(signed = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_reinterpret_:_signed">signed</code>
</td>
<td>
If <code>TRUE</code> (default), reinterpret into Int64. Otherwise, it
will be reinterpreted in UInt64.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(x = 1:5, schema = list(x = pl$Int64))
df$select(pl$all()$reinterpret())
```

    #> shape: (5, 1)
    #> ┌─────┐
    #> │ x   │
    #> │ --- │
    #> │ i64 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> │ 4   │
    #> │ 5   │
    #> └─────┘
