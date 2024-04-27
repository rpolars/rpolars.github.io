

# Check inequality without <code>null</code> propagation

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L492)

## Description

Method equivalent of addition operator <code>expr + other</code>.

## Usage

<pre><code class='language-R'>Expr_neq_missing(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="other">other</code>
</td>
<td>
numeric or string value; accepts expression input.
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
