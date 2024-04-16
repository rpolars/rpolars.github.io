

# Apply logical AND on a column

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__expr.R#L582)

## Description

Check if all values in a Boolean column are <code>TRUE</code>. This
method is an expression - not to be confused with <code>pl$all()</code>
which is a function to select all columns.

## Usage

<pre><code class='language-R'>Expr_all(drop_nulls = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_all_:_drop_nulls">drop_nulls</code>
</td>
<td>
Logical. Default TRUE, as name says.
</td>
</tr>
</table>

## Value

Boolean literal

## Examples

``` r
library(polars)

pl$DataFrame(
  all = c(TRUE, TRUE),
  any = c(TRUE, FALSE),
  none = c(FALSE, FALSE)
)$select(
  # the first $all() selects all columns, the second one applies the AND
  # logical on the values
  pl$all()$all()
)
```

    #> shape: (1, 3)
    #> ┌──────┬───────┬───────┐
    #> │ all  ┆ any   ┆ none  │
    #> │ ---  ┆ ---   ┆ ---   │
    #> │ bool ┆ bool  ┆ bool  │
    #> ╞══════╪═══════╪═══════╡
    #> │ true ┆ false ┆ false │
    #> └──────┴───────┴───────┘
