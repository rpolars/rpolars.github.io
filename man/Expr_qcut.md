

# Bin continuous values into discrete categories based on their quantiles

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3492)

## Description

Bin continuous values into discrete categories based on their quantiles

## Usage

<pre><code class='language-R'>Expr_qcut(
  quantiles,
  ...,
  labels = NULL,
  left_closed = FALSE,
  allow_duplicates = FALSE,
  include_breaks = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_qcut_:_quantiles">quantiles</code>
</td>
<td>
Either a vector of quantile probabilities between 0 and 1 or a positive
integer determining the number of bins with uniform probability.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_qcut_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_qcut_:_labels">labels</code>
</td>
<td>
Names of the categories. The number of labels must be equal to the
number of cut points plus one.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_qcut_:_left_closed">left_closed</code>
</td>
<td>
Set the intervals to be left-closed instead of right-closed.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_qcut_:_allow_duplicates">allow_duplicates</code>
</td>
<td>
If set to <code>TRUE</code>, duplicates in the resulting quantiles are
dropped, rather than raising an error. This can happen even with unique
probabilities, depending on the data.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_qcut_:_include_breaks">include_breaks</code>
</td>
<td>
Include a column with the right endpoint of the bin each observation
falls in. This will change the data type of the output from a
<code>Categorical</code> to a <code>Struct</code>.
</td>
</tr>
</table>

## Value

Expr of data type <code>Categorical</code> is
<code>include_breaks</code> is <code>FALSE</code> and of data type
<code>Struct</code> if <code>include_breaks</code> is <code>TRUE</code>.

## See Also

<code>$cut()</code>

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c(-2, -1, 0, 1, 2))

# Divide a column into three categories according to pre-defined quantile
# probabilities
df$with_columns(
  qcut = pl$col("foo")$qcut(c(0.25, 0.75), labels = c("a", "b", "c"))
)
```

    #> shape: (5, 2)
    #> ┌──────┬──────┐
    #> │ foo  ┆ qcut │
    #> │ ---  ┆ ---  │
    #> │ f64  ┆ cat  │
    #> ╞══════╪══════╡
    #> │ -2.0 ┆ a    │
    #> │ -1.0 ┆ a    │
    #> │ 0.0  ┆ b    │
    #> │ 1.0  ┆ b    │
    #> │ 2.0  ┆ c    │
    #> └──────┴──────┘

``` r
# Divide a column into two categories using uniform quantile probabilities.
df$with_columns(
  qcut = pl$col("foo")$qcut(2, labels = c("low", "high"), left_closed = TRUE)
)
```

    #> shape: (5, 2)
    #> ┌──────┬──────┐
    #> │ foo  ┆ qcut │
    #> │ ---  ┆ ---  │
    #> │ f64  ┆ cat  │
    #> ╞══════╪══════╡
    #> │ -2.0 ┆ low  │
    #> │ -1.0 ┆ low  │
    #> │ 0.0  ┆ high │
    #> │ 1.0  ┆ high │
    #> │ 2.0  ┆ high │
    #> └──────┴──────┘

``` r
# Add both the category and the breakpoint
df$with_columns(
  qcut = pl$col("foo")$qcut(c(0.25, 0.75), include_breaks = TRUE)
)$unnest("qcut")
```

    #> shape: (5, 3)
    #> ┌──────┬──────┬────────────┐
    #> │ foo  ┆ brk  ┆ foo_bin    │
    #> │ ---  ┆ ---  ┆ ---        │
    #> │ f64  ┆ f64  ┆ cat        │
    #> ╞══════╪══════╪════════════╡
    #> │ -2.0 ┆ -1.0 ┆ (-inf, -1] │
    #> │ -1.0 ┆ -1.0 ┆ (-inf, -1] │
    #> │ 0.0  ┆ 1.0  ┆ (-1, 1]    │
    #> │ 1.0  ┆ 1.0  ┆ (-1, 1]    │
    #> │ 2.0  ┆ inf  ┆ (1, inf]   │
    #> └──────┴──────┴────────────┘
