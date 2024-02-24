

# Difference

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2804)

## Description

Calculate the n-th discrete difference.

## Usage

<pre><code class='language-R'>Expr_diff(n = 1, null_behavior = c("ignore", "drop"))
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_diff_:_n">n</code>
</td>
<td>
Number of slots to shift.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_diff_:_null_behavior">null_behavior</code>
</td>
<td>
String, either <code>“ignore”</code> (default), else
<code>“drop”</code>.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(20L, 10L, 30L, 40L))$with_columns(
  diff_default = pl$col("a")$diff(),
  diff_2_ignore = pl$col("a")$diff(2, "ignore")
)
```

    #> shape: (4, 3)
    #> ┌─────┬──────────────┬───────────────┐
    #> │ a   ┆ diff_default ┆ diff_2_ignore │
    #> │ --- ┆ ---          ┆ ---           │
    #> │ i32 ┆ i32          ┆ i32           │
    #> ╞═════╪══════════════╪═══════════════╡
    #> │ 20  ┆ null         ┆ null          │
    #> │ 10  ┆ -10          ┆ null          │
    #> │ 30  ┆ 20           ┆ 10            │
    #> │ 40  ┆ 10           ┆ 30            │
    #> └─────┴──────────────┴───────────────┘
