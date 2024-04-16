

# Compute the logarithm of elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__expr.R#L3102)

## Description

Compute the logarithm of elements

## Usage

<pre><code class='language-R'>Expr_log(base = base::exp(1))
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_log_:_base">base</code>
</td>
<td>
Numeric base value for logarithm, default is <code>exp(1)</code>.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(1, 2, 3, exp(1)))$
  with_columns(log = pl$col("a")$log())
```

    #> shape: (4, 2)
    #> ┌──────────┬──────────┐
    #> │ a        ┆ log      │
    #> │ ---      ┆ ---      │
    #> │ f64      ┆ f64      │
    #> ╞══════════╪══════════╡
    #> │ 1.0      ┆ 0.0      │
    #> │ 2.0      ┆ 0.693147 │
    #> │ 3.0      ┆ 1.098612 │
    #> │ 2.718282 ┆ 1.0      │
    #> └──────────┴──────────┘
