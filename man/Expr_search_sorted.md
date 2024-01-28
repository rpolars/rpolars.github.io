

# Where to inject element(s) to maintain sorting

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__expr.R#L1497)

## Description

Find the index in self where the element should be inserted so that it
doesn’t break sortedness.

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
Expr or scalar value.
</td>
</tr>
</table>

## Details

This function looks up where to insert element to keep self column
sorted. It is assumed the self column is already sorted in ascending
order (otherwise this leads to wrong results).

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
df$select(pl$col("a")$search_sorted(5))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 4   │
    #> └─────┘
