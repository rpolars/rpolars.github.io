
# Rank elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2668)

## Description

Assign ranks to data, dealing with ties appropriately.

## Usage

<pre><code class='language-R'>Expr_rank(method = "average", descending = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rank_:_method">method</code>
</td>
<td>

String, one of <code>“average”</code> (default), <code>“min”</code>,
<code>“max”</code>, <code>“dense”</code>, <code>“ordinal”</code>,
<code>“random”</code>. The method used to assign ranks to tied elements:

<ul>
<li>

<code>“average”</code>: The average of the ranks that would have been
assigned to all the tied values is assigned to each value.

</li>
<li>

<code>“min”</code>: The minimum of the ranks that would have been
assigned to all the tied values is assigned to each value. (This is also
referred to as "competition" ranking.)

</li>
<li>

<code>“max”</code> : The maximum of the ranks that would have been
assigned to all the tied values is assigned to each value.

</li>
<li>

<code>“dense”</code>: Like ‘min’, but the rank of the next highest
element is assigned the rank immediately after those assigned to the
tied elements.

</li>
<li>

<code>“ordinal”</code> : All values are given a distinct rank,
corresponding to the order that the values occur in the Series.

</li>
<li>

<code>“random”</code> : Like ‘ordinal’, but the rank for ties is not
dependent on the order that the values occur in the Series.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rank_:_descending">descending</code>
</td>
<td>
Rank in descending order.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

#  The 'average' method:
pl$DataFrame(a = c(3, 6, 1, 1, 6))$
  with_columns(rank = pl$col("a")$rank())
```

    #> shape: (5, 2)
    #> ┌─────┬──────┐
    #> │ a   ┆ rank │
    #> │ --- ┆ ---  │
    #> │ f64 ┆ f64  │
    #> ╞═════╪══════╡
    #> │ 3.0 ┆ 3.0  │
    #> │ 6.0 ┆ 4.5  │
    #> │ 1.0 ┆ 1.5  │
    #> │ 1.0 ┆ 1.5  │
    #> │ 6.0 ┆ 4.5  │
    #> └─────┴──────┘

``` r
#  The 'ordinal' method:
pl$DataFrame(a = c(3, 6, 1, 1, 6))$
  with_columns(rank = pl$col("a")$rank("ordinal"))
```

    #> shape: (5, 2)
    #> ┌─────┬──────┐
    #> │ a   ┆ rank │
    #> │ --- ┆ ---  │
    #> │ f64 ┆ u32  │
    #> ╞═════╪══════╡
    #> │ 3.0 ┆ 3    │
    #> │ 6.0 ┆ 4    │
    #> │ 1.0 ┆ 1    │
    #> │ 1.0 ┆ 2    │
    #> │ 6.0 ┆ 5    │
    #> └─────┴──────┘
