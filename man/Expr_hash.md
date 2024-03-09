

# Hash elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/expr__expr.R#L2158)

## Description

The hash value is of type <code>UInt64</code>.

## Usage

<pre><code class='language-R'>Expr_hash(seed = 0, seed_1 = NULL, seed_2 = NULL, seed_3 = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_hash_:_seed">seed</code>
</td>
<td>
Random seed parameter. Defaults to 0. Doesn’t have any effect for now.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_hash_:_seed_1">seed_1</code>,
<code id="Expr_hash_:_seed_2">seed_2</code>,
<code id="Expr_hash_:_seed_3">seed_3</code>
</td>
<td>
Random seed parameter. Defaults to arg seed. The column will be coerced
to UInt32.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(iris[1:3, c(1, 2)])
df$with_columns(pl$all()$hash(1234)$name$suffix("_hash"))
```

    #> shape: (3, 4)
    #> ┌──────────────┬─────────────┬──────────────────────┬──────────────────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Sepal.Length_hash    ┆ Sepal.Width_hash     │
    #> │ ---          ┆ ---         ┆ ---                  ┆ ---                  │
    #> │ f64          ┆ f64         ┆ u64                  ┆ u64                  │
    #> ╞══════════════╪═════════════╪══════════════════════╪══════════════════════╡
    #> │ 5.1          ┆ 3.5         ┆ 18232672881806689409 ┆ 14554506282174058345 │
    #> │ 4.9          ┆ 3.0         ┆ 8623783022495418418  ┆ 8050606693503481463  │
    #> │ 4.7          ┆ 3.2         ┆ 18174443662047712936 ┆ 13738524453008131871 │
    #> └──────────────┴─────────────┴──────────────────────┴──────────────────────┘
