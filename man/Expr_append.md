
# Append expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__expr.R#L1225)

## Description

This is done by adding the chunks of <code>other</code> to this
<code>output</code>.

## Usage

<pre><code class='language-R'>Expr_append(other, upcast = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_append_:_other">other</code>
</td>
<td>
Expr or something coercible to an Expr.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_append_:_upcast">upcast</code>
</td>
<td>
Cast both Expr to a common supertype if they have one.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

# append bottom to to row
df = pl$DataFrame(list(a = 1:3, b = c(NA_real_, 4, 5)))
df$select(pl$all()$head(1)$append(pl$all()$tail(1)))
```

    #> shape: (2, 2)
    #> ┌─────┬──────┐
    #> │ a   ┆ b    │
    #> │ --- ┆ ---  │
    #> │ i32 ┆ f64  │
    #> ╞═════╪══════╡
    #> │ 1   ┆ null │
    #> │ 3   ┆ 5.0  │
    #> └─────┴──────┘

``` r
# implicit upcast, when default = TRUE
pl$DataFrame(list())$select(pl$lit(42)$append(42L))
```

    #> shape: (2, 1)
    #> ┌─────────┐
    #> │ literal │
    #> │ ---     │
    #> │ f64     │
    #> ╞═════════╡
    #> │ 42.0    │
    #> │ 42.0    │
    #> └─────────┘

``` r
pl$DataFrame(list())$select(pl$lit(42)$append(FALSE))
```

    #> shape: (2, 1)
    #> ┌─────────┐
    #> │ literal │
    #> │ ---     │
    #> │ f64     │
    #> ╞═════════╡
    #> │ 42.0    │
    #> │ 0.0     │
    #> └─────────┘

``` r
pl$DataFrame(list())$select(pl$lit("Bob")$append(FALSE))
```

    #> shape: (2, 1)
    #> ┌─────────┐
    #> │ literal │
    #> │ ---     │
    #> │ str     │
    #> ╞═════════╡
    #> │ Bob     │
    #> │ false   │
    #> └─────────┘
