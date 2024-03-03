

# Apply logical OR on a column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L599)

## Description

Check if any boolean value in a Boolean column is <code>TRUE</code>.

## Usage

<pre><code class='language-R'>Expr_any(drop_nulls = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_any_:_drop_nulls">drop_nulls</code>
</td>
<td>
Boolean. Default TRUE, as name says.
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
  pl$all()$any()
)
```

    #> shape: (1, 3)
    #> ┌──────┬──────┬───────┐
    #> │ all  ┆ any  ┆ none  │
    #> │ ---  ┆ ---  ┆ ---   │
    #> │ bool ┆ bool ┆ bool  │
    #> ╞══════╪══════╪═══════╡
    #> │ true ┆ true ┆ false │
    #> └──────┴──────┴───────┘
