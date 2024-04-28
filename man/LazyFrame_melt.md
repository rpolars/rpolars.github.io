

# Unpivot a Frame from wide to long format

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1478)

## Description

Unpivot a Frame from wide to long format

## Usage

<pre><code class='language-R'>LazyFrame_melt(
  id_vars = NULL,
  value_vars = NULL,
  variable_name = NULL,
  value_name = NULL,
  ...,
  streamable = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="id_vars">id_vars</code>
</td>
<td>
Columns to use as identifier variables.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="value_vars">value_vars</code>
</td>
<td>
Values to use as identifier variables. If <code>value_vars</code> is
empty all columns that are not in <code>id_vars</code> will be used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="variable_name">variable_name</code>
</td>
<td>
Name to give to the new column containing the names of the melted
columns. Defaults to "variable".
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="value_name">value_name</code>
</td>
<td>
Name to give to the new column containing the values of the melted
columns. Defaults to "value"
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="streamable">streamable</code>
</td>
<td>
Allow this node to run in the streaming engine. If this runs in
streaming, the output of the melt operation will not have a stable
ordering.
</td>
</tr>
</table>

## Details

Optionally leaves identifiers set.

This function is useful to massage a Frame into a format where one or
more columns are identifier variables (id_vars), while all other
columns, considered measured variables (value_vars), are "unpivoted" to
the row axis, leaving just two non-identifier columns, ‘variable’ and
‘value’.

## Value

A LazyFrame

## Examples

``` r
library(polars)

lf = pl$LazyFrame(
  a = c("x", "y", "z"),
  b = c(1, 3, 5),
  c = c(2, 4, 6)
)
lf$melt(id_vars = "a", value_vars = c("b", "c"))$collect()
```

    #> shape: (6, 3)
    #> ┌─────┬──────────┬───────┐
    #> │ a   ┆ variable ┆ value │
    #> │ --- ┆ ---      ┆ ---   │
    #> │ str ┆ str      ┆ f64   │
    #> ╞═════╪══════════╪═══════╡
    #> │ x   ┆ b        ┆ 1.0   │
    #> │ y   ┆ b        ┆ 3.0   │
    #> │ z   ┆ b        ┆ 5.0   │
    #> │ x   ┆ c        ┆ 2.0   │
    #> │ y   ┆ c        ┆ 4.0   │
    #> │ z   ┆ c        ┆ 6.0   │
    #> └─────┴──────────┴───────┘
