

# Apply the OR logical rowwise

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/functions__lazy.R#L996)

## Description

Apply the OR logical rowwise

## Usage

<pre><code class='language-R'>pl_any_horizontal(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_any_horizontal_:_...">…</code>
</td>
<td>
Columns to concatenate into a single string column. Accepts expressions.
Strings are parsed as column names, other non-expression inputs are
parsed as literals.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(FALSE, FALSE, NA, NA),
  b = c(TRUE, FALSE, NA, NA),
  c = c(TRUE, FALSE, NA, TRUE)
)
df
```

    #> shape: (4, 3)
    #> ┌───────┬───────┬───────┐
    #> │ a     ┆ b     ┆ c     │
    #> │ ---   ┆ ---   ┆ ---   │
    #> │ bool  ┆ bool  ┆ bool  │
    #> ╞═══════╪═══════╪═══════╡
    #> │ false ┆ true  ┆ true  │
    #> │ false ┆ false ┆ false │
    #> │ null  ┆ null  ┆ null  │
    #> │ null  ┆ null  ┆ true  │
    #> └───────┴───────┴───────┘

``` r
df$with_columns(
  pl$any_horizontal("a", "b", "c")$alias("any")
)
```

    #> shape: (4, 4)
    #> ┌───────┬───────┬───────┬───────┐
    #> │ a     ┆ b     ┆ c     ┆ any   │
    #> │ ---   ┆ ---   ┆ ---   ┆ ---   │
    #> │ bool  ┆ bool  ┆ bool  ┆ bool  │
    #> ╞═══════╪═══════╪═══════╪═══════╡
    #> │ false ┆ true  ┆ true  ┆ true  │
    #> │ false ┆ false ┆ false ┆ false │
    #> │ null  ┆ null  ┆ null  ┆ null  │
    #> │ null  ┆ null  ┆ true  ┆ true  │
    #> └───────┴───────┴───────┴───────┘

``` r
# drop rows that only have missing values == keep rows that have at least one
# non-missing value
df$filter(
  pl$any_horizontal(pl$all()$is_not_null())
)
```

    #> shape: (3, 3)
    #> ┌───────┬───────┬───────┐
    #> │ a     ┆ b     ┆ c     │
    #> │ ---   ┆ ---   ┆ ---   │
    #> │ bool  ┆ bool  ┆ bool  │
    #> ╞═══════╪═══════╪═══════╡
    #> │ false ┆ true  ┆ true  │
    #> │ false ┆ false ┆ false │
    #> │ null  ┆ null  ┆ true  │
    #> └───────┴───────┴───────┘
