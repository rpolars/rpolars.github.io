
# Unpivot a Frame from wide to long format

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1352)

## Description

Unpivot a Frame from wide to long format

## Usage

<pre><code class='language-R'>DataFrame_melt(
  id_vars = NULL,
  value_vars = NULL,
  variable_name = NULL,
  value_name = NULL
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_melt_:_id_vars">id_vars</code>
</td>
<td>
Columns to use as identifier variables.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_melt_:_value_vars">value_vars</code>
</td>
<td>
Values to use as identifier variables. If <code>value_vars</code> is
empty all columns that are not in <code>id_vars</code> will be used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_melt_:_variable_name">variable_name</code>
</td>
<td>
Name to give to the new column containing the names of the melted
columns. Defaults to "variable".
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_melt_:_value_name">value_name</code>
</td>
<td>
Name to give to the new column containing the values of the melted
columns. Defaults to "value"
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

A new <code>DataFrame</code>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c("x", "y", "z"),
  b = c(1, 3, 5),
  c = c(2, 4, 6),
  d = c(7, 8, 9)
)
df$melt(id_vars = "a", value_vars = c("b", "c", "d"))
```

    #> shape: (9, 3)
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
    #> │ x   ┆ d        ┆ 7.0   │
    #> │ y   ┆ d        ┆ 8.0   │
    #> │ z   ┆ d        ┆ 9.0   │
    #> └─────┴──────────┴───────┘
