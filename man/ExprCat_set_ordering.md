

# Set Ordering

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__categorical.R#L26)

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
)

# sort by the string value of categories
df$with_columns(
  pl$col("cats")$cat$set_ordering("lexical")
)$sort("cats", "vals")
```

    #> shape: (5, 2)
    #> ┌──────┬──────┐
    #> │ cats ┆ vals │
    #> │ ---  ┆ ---  │
    #> │ cat  ┆ f64  │
    #> ╞══════╪══════╡
    #> │ a    ┆ 2.0  │
    #> │ b    ┆ 3.0  │
    #> │ k    ┆ 2.0  │
    #> │ z    ┆ 1.0  │
    #> │ z    ┆ 3.0  │
    #> └──────┴──────┘

``` r
# sort by the underlying value of categories
df$with_columns(
  pl$col("cats")$cat$set_ordering("physical")
)$sort("cats", "vals")
```

    #> shape: (5, 2)
    #> ┌──────┬──────┐
    #> │ cats ┆ vals │
    #> │ ---  ┆ ---  │
    #> │ cat  ┆ f64  │
    #> ╞══════╪══════╡
    #> │ z    ┆ 1.0  │
    #> │ z    ┆ 3.0  │
    #> │ k    ┆ 2.0  │
    #> │ a    ┆ 2.0  │
    #> │ b    ┆ 3.0  │
    #> └──────┴──────┘
