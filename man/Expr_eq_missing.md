

# Check equality without <code>null</code> propagation

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L452)

## Description

Method equivalent of addition operator <code>expr + other</code>.

## Usage

<pre><code class='language-R'>Expr_eq_missing(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_eq_missing_:_other">other</code>
</td>
<td>
numeric or string value; accepts expression input.
</td>
</tr>
</table>

## Value

Expr

## See Also

Expr_eq

## Examples

``` r
library(polars)

df = pl$DataFrame(x = c(NA, FALSE, TRUE), y = c(TRUE, TRUE, TRUE))
df$with_columns(
  eq = pl$col("x")$eq("y"),
  eq_missing = pl$col("x")$eq_missing("y")
)
```

    #> shape: (3, 4)
    #> ┌───────┬──────┬───────┬────────────┐
    #> │ x     ┆ y    ┆ eq    ┆ eq_missing │
    #> │ ---   ┆ ---  ┆ ---   ┆ ---        │
    #> │ bool  ┆ bool ┆ bool  ┆ bool       │
    #> ╞═══════╪══════╪═══════╪════════════╡
    #> │ null  ┆ true ┆ null  ┆ false      │
    #> │ false ┆ true ┆ false ┆ false      │
    #> │ true  ┆ true ┆ false ┆ false      │
    #> └───────┴──────┴───────┴────────────┘
