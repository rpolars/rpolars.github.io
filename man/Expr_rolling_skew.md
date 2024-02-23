

# Rolling skew

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__expr.R#L2637)

## Description

Compute the rolling (= moving) skewness over the values in this array. A
window of length <code>window_size</code> will traverse the array.

## Usage

<pre><code class='language-R'>Expr_rolling_skew(window_size, bias = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rolling_skew_:_window_size">window_size</code>
</td>
<td>

The length of the window. Can be a fixed integer size, or a dynamic
temporal size indicated by the following string language:

<ul>
<li>

1ns (1 nanosecond)

</li>
<li>

1us (1 microsecond)

</li>
<li>

1ms (1 millisecond)

</li>
<li>

1s (1 second)

</li>
<li>

1m (1 minute)

</li>
<li>

1h (1 hour)

</li>
<li>

1d (1 day)

</li>
<li>

1w (1 week)

</li>
<li>

1mo (1 calendar month)

</li>
<li>

1y (1 calendar year)

</li>
<li>

1i (1 index count) If the dynamic string language is used, the
<code>by</code> and <code>closed</code> arguments must also be set.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rolling_skew_:_bias">bias</code>
</td>
<td>
If <code>FALSE</code>, the calculations are corrected for statistical
bias.
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

pl$DataFrame(a = c(1, 3, 2, 4, 5, 6))$
  with_columns(roll_skew = pl$col("a")$rolling_skew(window_size = 2))
```

    #> shape: (6, 2)
    #> ┌─────┬───────────┐
    #> │ a   ┆ roll_skew │
    #> │ --- ┆ ---       │
    #> │ f64 ┆ f64       │
    #> ╞═════╪═══════════╡
    #> │ 1.0 ┆ null      │
    #> │ 3.0 ┆ 0.0       │
    #> │ 2.0 ┆ 0.0       │
    #> │ 4.0 ┆ 0.0       │
    #> │ 5.0 ┆ 0.0       │
    #> │ 6.0 ┆ 0.0       │
    #> └─────┴───────────┘
