

# Horizontally concatenate columns into a single string column

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/functions__lazy.R#L764)

## Description

Horizontally concatenate columns into a single string column

## Usage

<pre><code class='language-R'>pl_concat_str(..., separator = "")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_concat_str_:_...">…</code>
</td>
<td>
Columns to concatenate into a single string column. Accepts expressions.
Strings are parsed as column names, other non-expression inputs are
parsed as literals. Non-String columns are cast to String
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_concat_str_:_separator">separator</code>
</td>
<td>
String that will be used to separate the values of each column.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1, 2, 3),
  b = c("dogs", "cats", NA),
  c = c("play", "swim", "walk")
)

df$with_columns(
  pl$concat_str(
    pl$col("a") * 2,
    "b",
    "c",
    pl$lit("!"),
    separator = " "
  )$alias("full_sentence")
)
```

    #> shape: (3, 4)
    #> ┌─────┬──────┬──────┬─────────────────┐
    #> │ a   ┆ b    ┆ c    ┆ full_sentence   │
    #> │ --- ┆ ---  ┆ ---  ┆ ---             │
    #> │ f64 ┆ str  ┆ str  ┆ str             │
    #> ╞═════╪══════╪══════╪═════════════════╡
    #> │ 1.0 ┆ dogs ┆ play ┆ 2.0 dogs play ! │
    #> │ 2.0 ┆ cats ┆ swim ┆ 4.0 cats swim ! │
    #> │ 3.0 ┆ null ┆ walk ┆ null            │
    #> └─────┴──────┴──────┴─────────────────┘
