

# Bin continuous values into discrete categories

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L3451)

## Description

Bin continuous values into discrete categories

## Usage

<pre><code class='language-R'>Expr_cut(
  breaks,
  ...,
  labels = NULL,
  left_closed = FALSE,
  include_breaks = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="breaks">breaks</code>
</td>
<td>
Unique cut points.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="labels">labels</code>
</td>
<td>
Names of the categories. The number of labels must be equal to the
number of cut points plus one.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="left_closed">left_closed</code>
</td>
<td>
Set the intervals to be left-closed instead of right-closed.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="include_breaks">include_breaks</code>
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

<code>$qcut()</code>

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c(-2, -1, 0, 1, 2))

df$with_columns(
  cut = pl$col("foo")$cut(c(-1, 1), labels = c("a", "b", "c"))
)
```

    #> shape: (5, 2)
    #> ┌──────┬─────┐
    #> │ foo  ┆ cut │
    #> │ ---  ┆ --- │
    #> │ f64  ┆ cat │
    #> ╞══════╪═════╡
    #> │ -2.0 ┆ a   │
    #> │ -1.0 ┆ a   │
    #> │ 0.0  ┆ b   │
    #> │ 1.0  ┆ b   │
    #> │ 2.0  ┆ c   │
    #> └──────┴─────┘

``` r
# Add both the category and the breakpoint
df$with_columns(
  cut = pl$col("foo")$cut(c(-1, 1), include_breaks = TRUE)
)$unnest("cut")
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
