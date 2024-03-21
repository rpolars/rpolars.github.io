

# Add an external context to the computation graph

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1803)

## Description

This allows expressions to also access columns from DataFrames or
LazyFrames that are not part of this one.

## Usage

<pre><code class='language-R'>LazyFrame_with_context(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_with_context_:_other">other</code>
</td>
<td>
Data/LazyFrame to have access to. This can be a list of DataFrames and
LazyFrames.
</td>
</tr>
</table>

## Value

A LazyFrame

## Examples

``` r
library(polars)

lf = pl$LazyFrame(a = c(1, 2, 3), b = c("a", "c", NA))
lf_other = pl$LazyFrame(c = c("foo", "ham"))

lf$with_context(lf_other)$select(
  pl$col("b") + pl$col("c")$first()
)$collect()
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ b    │
    #> │ ---  │
    #> │ str  │
    #> ╞══════╡
    #> │ afoo │
    #> │ cfoo │
    #> │ null │
    #> └──────┘

``` r
# Fill nulls with the median from another lazyframe:
train_lf = pl$LazyFrame(
  feature_0 = c(-1.0, 0, 1), feature_1 = c(-1.0, 0, 1)
)
test_lf = pl$LazyFrame(
  feature_0 = c(-1.0, NA, 1), feature_1 = c(-1.0, 0, 1)
)

test_lf$with_context(train_lf$select(pl$all()$name$suffix("_train")))$select(
  pl$col("feature_0")$fill_null(pl$col("feature_0_train")$median())
)$collect()
```

    #> shape: (3, 1)
    #> ┌───────────┐
    #> │ feature_0 │
    #> │ ---       │
    #> │ f64       │
    #> ╞═══════════╡
    #> │ -1.0      │
    #> │ 0.0       │
    #> │ 1.0       │
    #> └───────────┘
