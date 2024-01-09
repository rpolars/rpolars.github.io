
# Check inequality without <code>null</code> propagation

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__expr.R#L389)

## Description

The RHS can either be an Expr or an object that can be converted to a
literal (e.g an integer).

## Usage

<pre><code class='language-R'>Expr_neq_missing(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_neq_missing_:_other">other</code>
</td>
<td>
Literal or object that can be converted to a literal
</td>
</tr>
</table>

## Value

Expr

## See Also

Expr_neq

## Examples

``` r
library(polars)

df = pl$DataFrame(x = c(NA, FALSE, TRUE), y = c(TRUE, TRUE, TRUE))
df$with_columns(
  neq = pl$col("x")$neq("y"),
  neq_missing = pl$col("x")$neq_missing("y")
)
```

    #> shape: (3, 4)
    #> ┌───────┬──────┬──────┬─────────────┐
    #> │ x     ┆ y    ┆ neq  ┆ neq_missing │
    #> │ ---   ┆ ---  ┆ ---  ┆ ---         │
    #> │ bool  ┆ bool ┆ bool ┆ bool        │
    #> ╞═══════╪══════╪══════╪═════════════╡
    #> │ null  ┆ true ┆ null ┆ true        │
    #> │ false ┆ true ┆ true ┆ true        │
    #> │ true  ┆ true ┆ true ┆ true        │
    #> └───────┴──────┴──────┴─────────────┘
