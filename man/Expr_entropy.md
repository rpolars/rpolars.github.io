

# Entropy

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3130)

## Description

The entropy is measured with the formula <code>-sum(pk \*
log(pk))</code> where <code>pk</code> are discrete probabilities.

## Usage

<pre><code class='language-R'>Expr_entropy(base = base::exp(1), normalize = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_entropy_:_base">base</code>
</td>
<td>
Given exponential base, defaults to <code>exp(1)</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_entropy_:_normalize">normalize</code>
</td>
<td>
Normalize <code>pk</code> if it doesn’t sum to 1.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1, 2, 3, 2))$
  with_columns(entropy = pl$col("x")$entropy(base = 2))
```

    #> shape: (4, 2)
    #> ┌─────┬──────────┐
    #> │ x   ┆ entropy  │
    #> │ --- ┆ ---      │
    #> │ f64 ┆ f64      │
    #> ╞═════╪══════════╡
    #> │ 1.0 ┆ 1.905639 │
    #> │ 2.0 ┆ 1.905639 │
    #> │ 3.0 ┆ 1.905639 │
    #> │ 2.0 ┆ 1.905639 │
    #> └─────┴──────────┘
