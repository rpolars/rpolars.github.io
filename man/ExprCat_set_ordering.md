
# Set Ordering

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__categorical.R#L19)

## Description

Determine how this categorical series should be sorted.

## Usage

<pre><code class='language-R'>ExprCat_set_ordering(ordering)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprCat_set_ordering_:_ordering">ordering</code>
</td>
<td>

string either ‘physical’ or ‘lexical’

<ul>
<li>

‘physical’ -\> Use the physical representation of the categories to
determine the order (default).

</li>
<li>

‘lexical’ -\> Use the string values to determine the ordering.

</li>
</ul>
</td>
</tr>
</table>

## Value

bool: TRUE if equal

## Examples

``` r
library(polars)

df = pl$DataFrame(
  cats = factor(c("z", "z", "k", "a", "b")),
  vals = c(3, 1, 2, 2, 3)
)$with_columns(
  pl$col("cats")$cat$set_ordering("physical")
)
df$select(pl$all()$sort())
```

    #> shape: (5, 2)
    #> ┌──────┬──────┐
    #> │ cats ┆ vals │
    #> │ ---  ┆ ---  │
    #> │ cat  ┆ f64  │
    #> ╞══════╪══════╡
    #> │ z    ┆ 1.0  │
    #> │ z    ┆ 2.0  │
    #> │ k    ┆ 2.0  │
    #> │ a    ┆ 3.0  │
    #> │ b    ┆ 3.0  │
    #> └──────┴──────┘
