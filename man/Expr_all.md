

# Apply logical AND on a column

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L582)

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
<code id="drop_nulls">drop_nulls</code>
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
