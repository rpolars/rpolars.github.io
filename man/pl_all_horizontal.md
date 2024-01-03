
# Apply the AND logical rowwise

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L950)

## Description

Apply the AND logical rowwise

## Usage

<pre><code class='language-R'>pl_all_horizontal(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_all_horizontal_:_...">…</code>
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
  a = c(TRUE, FALSE, NA, NA),
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
    #> │ true  ┆ true  ┆ true  │
    #> │ false ┆ false ┆ false │
    #> │ null  ┆ null  ┆ null  │
    #> │ null  ┆ null  ┆ true  │
    #> └───────┴───────┴───────┘

``` r
df$with_columns(
  pl$all_horizontal("a", "b", "c")$alias("all")
)
```

    #> shape: (4, 4)
    #> ┌───────┬───────┬───────┬───────┐
    #> │ a     ┆ b     ┆ c     ┆ all   │
    #> │ ---   ┆ ---   ┆ ---   ┆ ---   │
    #> │ bool  ┆ bool  ┆ bool  ┆ bool  │
    #> ╞═══════╪═══════╪═══════╪═══════╡
    #> │ true  ┆ true  ┆ true  ┆ true  │
    #> │ false ┆ false ┆ false ┆ false │
    #> │ null  ┆ null  ┆ null  ┆ null  │
    #> │ null  ┆ null  ┆ true  ┆ null  │
    #> └───────┴───────┴───────┴───────┘

``` r
# drop rows that have at least one missing value
# == keep rows that only have non-missing values
df$filter(
  pl$all_horizontal(pl$all()$is_not_null())
)
```

    #> shape: (2, 3)
    #> ┌───────┬───────┬───────┐
    #> │ a     ┆ b     ┆ c     │
    #> │ ---   ┆ ---   ┆ ---   │
    #> │ bool  ┆ bool  ┆ bool  │
    #> ╞═══════╪═══════╪═══════╡
    #> │ true  ┆ true  ┆ true  │
    #> │ false ┆ false ┆ false │
    #> └───────┴───────┴───────┘
