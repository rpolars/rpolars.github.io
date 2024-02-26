

# Coalesce

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L487)

## Description

Folds the expressions from left to right, keeping the first non-null
value.

## Usage

<pre><code class='language-R'>pl_coalesce(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_coalesce_:_...">…</code>
</td>
<td>

is a: If one arg:

<ul>
<li>

Series or Expr, same as <code>column$sum()</code>

</li>
<li>

string, same as <code>pl$col(column)$sum()</code>

</li>
<li>

numeric, same as <code>pl$lit(column)$sum()</code>

</li>
<li>

list of strings(column names) or expressions to add up as expr1 +
expr2 + expr3 + …

</li>
</ul>
If several args, then wrapped in a list and handled as above.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = NA_real_,
  b = c(1:2, NA_real_, NA_real_),
  c = c(1:3, NA_real_)
)
# use coalesce to get first non Null value for each row, otherwise insert 99.9
df$with_columns(
  pl$coalesce("a", "b", "c", 99.9)$alias("d")
)
```

    #> shape: (4, 4)
    #> ┌──────┬──────┬──────┬──────┐
    #> │ a    ┆ b    ┆ c    ┆ d    │
    #> │ ---  ┆ ---  ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64  ┆ f64  ┆ f64  │
    #> ╞══════╪══════╪══════╪══════╡
    #> │ null ┆ 1.0  ┆ 1.0  ┆ 1.0  │
    #> │ null ┆ 2.0  ┆ 2.0  ┆ 2.0  │
    #> │ null ┆ null ┆ 3.0  ┆ 3.0  │
    #> │ null ┆ null ┆ null ┆ 99.9 │
    #> └──────┴──────┴──────┴──────┘
