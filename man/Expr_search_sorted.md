

# Where to inject element(s) to maintain sorting

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1537)

## Description

Find indices where elements should be inserted to maintain order.

## Usage

<pre><code class='language-R'>Expr_search_sorted(element)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_search_sorted_:_element">element</code>
</td>
<td>
Element to insert. Can be an Expr or something coercible to an Expr.
</td>
</tr>
</table>

## Details

This function looks up where to insert element to keep self column
sorted. It is assumed the column is already sorted in ascending order
(otherwise this leads to wrong results).

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c(1, 3, 4, 4, 6))
df
```

    #> shape: (5, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> │ 3.0 │
    #> │ 4.0 │
    #> │ 4.0 │
    #> │ 6.0 │
    #> └─────┘

``` r
# in which row should 5 be inserted in order to not break the sort?
# (value is 0-indexed)
df$select(
  zero = pl$col("a")$search_sorted(0),
  three = pl$col("a")$search_sorted(3),
  five = pl$col("a")$search_sorted(5)
)
```

    #> shape: (1, 3)
    #> ┌──────┬───────┬──────┐
    #> │ zero ┆ three ┆ five │
    #> │ ---  ┆ ---   ┆ ---  │
    #> │ u32  ┆ u32   ┆ u32  │
    #> ╞══════╪═══════╪══════╡
    #> │ 0    ┆ 1     ┆ 4    │
    #> └──────┴───────┴──────┘
