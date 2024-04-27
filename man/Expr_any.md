

# Apply logical OR on a column

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L600)

## Description

Check if any boolean value in a Boolean column is <code>TRUE</code>.

## Usage

<pre><code class='language-R'>Expr_any(drop_nulls = TRUE)
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
