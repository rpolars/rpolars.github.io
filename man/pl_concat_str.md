

# Horizontally concatenate columns into a single string column

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/functions__lazy.R#L702)

## Description

Horizontally concatenate columns into a single string column

## Usage

<pre><code class='language-R'>pl_concat_str(..., separator = "", ignore_nulls = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Columns to concatenate into a single string column. Accepts expressions.
Strings are parsed as column names, other non-expression inputs are
parsed as literals. Non-String columns are cast to String
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="separator">separator</code>
</td>
<td>
String that will be used to separate the values of each column.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ignore_nulls">ignore_nulls</code>
</td>
<td>
If <code>FALSE</code> (default), null values are propagated: if the row
contains any null values, the output is null.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = 1:3,
  b = c("dogs", "cats", NA),
  c = c("play", "swim", "walk")
)

df$with_columns(
  pl$concat_str(
    pl$col("a") * 2L, "b", "c", pl$lit("!"),
    separator = " "
  )$alias("full_sentence")
)
```

    #> shape: (3, 4)
    #> ┌─────┬──────┬──────┬───────────────┐
    #> │ a   ┆ b    ┆ c    ┆ full_sentence │
    #> │ --- ┆ ---  ┆ ---  ┆ ---           │
    #> │ i32 ┆ str  ┆ str  ┆ str           │
    #> ╞═════╪══════╪══════╪═══════════════╡
    #> │ 1   ┆ dogs ┆ play ┆ 2 dogs play ! │
    #> │ 2   ┆ cats ┆ swim ┆ 4 cats swim ! │
    #> │ 3   ┆ null ┆ walk ┆ null          │
    #> └─────┴──────┴──────┴───────────────┘

``` r
df$with_columns(
  pl$concat_str(
    pl$col("a") * 2L, "b", "c", pl$lit("!"),
    separator = " ",
    ignore_nulls = TRUE
  )$alias("full_sentence")
)
```

    #> shape: (3, 4)
    #> ┌─────┬──────┬──────┬───────────────┐
    #> │ a   ┆ b    ┆ c    ┆ full_sentence │
    #> │ --- ┆ ---  ┆ ---  ┆ ---           │
    #> │ i32 ┆ str  ┆ str  ┆ str           │
    #> ╞═════╪══════╪══════╪═══════════════╡
    #> │ 1   ┆ dogs ┆ play ┆ 2 dogs play ! │
    #> │ 2   ┆ cats ┆ swim ┆ 4 cats swim ! │
    #> │ 3   ┆ null ┆ walk ┆ 6 walk !      │
    #> └─────┴──────┴──────┴───────────────┘
