

# Skewness

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__expr.R#L2672)

## Description

Compute the sample skewness of a data set.

## Usage

<pre><code class='language-R'>Expr_skew(bias = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_skew_:_bias">bias</code>
</td>
<td>
If <code>FALSE</code>, then the calculations are corrected for
statistical bias.
</td>
</tr>
</table>

## Details

For normally distributed data, the skewness should be about zero. For
uni-modal continuous distributions, a skewness value greater than zero
means that there is more weight in the right tail of the distribution.

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = c(1:3, 2:1)))
df$select(pl$col("a")$skew())
```

    #> shape: (1, 1)
    #> ┌──────────┐
    #> │ a        │
    #> │ ---      │
    #> │ f64      │
    #> ╞══════════╡
    #> │ 0.343622 │
    #> └──────────┘
