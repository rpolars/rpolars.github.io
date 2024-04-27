

# Filter a single column.

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L1971)

## Description

Mostly useful in an aggregation context. If you want to filter on a
DataFrame level, use <code>DataFrame$filter()</code> (or
<code>LazyFrame$filter()</code>).

## Usage

<pre><code class='language-R'>Expr_filter(predicate)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="predicate">predicate</code>
</td>
<td>
An Expr or something coercible to an Expr. Must return a boolean.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  group_col = c("g1", "g1", "g2"),
  b = c(1, 2, 3)
)
df
```

    #> shape: (3, 2)
    #> ┌───────────┬─────┐
    #> │ group_col ┆ b   │
    #> │ ---       ┆ --- │
    #> │ str       ┆ f64 │
    #> ╞═══════════╪═════╡
    #> │ g1        ┆ 1.0 │
    #> │ g1        ┆ 2.0 │
    #> │ g2        ┆ 3.0 │
    #> └───────────┴─────┘

``` r
df$group_by("group_col")$agg(
  lt = pl$col("b")$filter(pl$col("b") < 2),
  gte = pl$col("b")$filter(pl$col("b") >= 2)
)
```

    #> shape: (2, 3)
    #> ┌───────────┬───────────┬───────────┐
    #> │ group_col ┆ lt        ┆ gte       │
    #> │ ---       ┆ ---       ┆ ---       │
    #> │ str       ┆ list[f64] ┆ list[f64] │
    #> ╞═══════════╪═══════════╪═══════════╡
    #> │ g2        ┆ []        ┆ [3.0]     │
    #> │ g1        ┆ [1.0]     ┆ [2.0]     │
    #> └───────────┴───────────┴───────────┘
