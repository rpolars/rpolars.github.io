
# Fill null values forward

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1683)

## Description

Fill missing values with the last seen values. Syntactic sugar for
<code style="white-space: pre;">$fill_null(strategy = “forward”)</code>.

## Usage

<pre><code class='language-R'>Expr_forward_fill(limit = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_forward_fill_:_limit">limit</code>
</td>
<td>
Number of consecutive null values to fill when using the
<code>“forward”</code> or <code>“backward”</code> strategy.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(NA, 1, NA, 2, NA))$
  with_columns(
  backward = pl$col("a")$forward_fill()
)
```

    #> shape: (5, 2)
    #> ┌──────┬──────────┐
    #> │ a    ┆ backward │
    #> │ ---  ┆ ---      │
    #> │ f64  ┆ f64      │
    #> ╞══════╪══════════╡
    #> │ null ┆ null     │
    #> │ 1.0  ┆ 1.0      │
    #> │ null ┆ 1.0      │
    #> │ 2.0  ┆ 2.0      │
    #> │ null ┆ 2.0      │
    #> └──────┴──────────┘
