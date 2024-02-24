

# Kurtosis

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2874)

## Description

Compute the kurtosis (Fisher or Pearson) of a dataset.

## Usage

<pre><code class='language-R'>Expr_kurtosis(fisher = TRUE, bias = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_kurtosis_:_fisher">fisher</code>
</td>
<td>
If <code>TRUE</code> (default), Fisher’s definition is used (normal,
centered at 0). Otherwise, Pearson’s definition is used (normal,
centered at 3).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_kurtosis_:_bias">bias</code>
</td>
<td>
If <code>FALSE</code>, the calculations are corrected for statistical
bias.
</td>
</tr>
</table>

## Details

Kurtosis is the fourth central moment divided by the square of the
variance. If Fisher’s definition is used, then 3 is subtracted from the
result to give 0 for a normal distribution.

If bias is <code>FALSE</code>, then the kurtosis is calculated using
<code>k</code> statistics to eliminate bias coming from biased moment
estimators.

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(1:3, 2:1))$
  with_columns(kurt = pl$col("a")$kurtosis())
```

    #> shape: (5, 2)
    #> ┌─────┬───────────┐
    #> │ a   ┆ kurt      │
    #> │ --- ┆ ---       │
    #> │ i32 ┆ f64       │
    #> ╞═════╪═══════════╡
    #> │ 1   ┆ -1.153061 │
    #> │ 2   ┆ -1.153061 │
    #> │ 3   ┆ -1.153061 │
    #> │ 2   ┆ -1.153061 │
    #> │ 1   ┆ -1.153061 │
    #> └─────┴───────────┘
