
# from_arrow

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/convert.R#L27)

## Description

import Arrow Table or Array

## Usage

<pre><code class='language-R'>pl_from_arrow(
  data,
  ...,
  rechunk = TRUE,
  schema = NULL,
  schema_overrides = NULL
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_from_arrow_:_data">data</code>
</td>
<td>
arrow Table or Array or ChunkedArray
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_from_arrow_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_from_arrow_:_rechunk">rechunk</code>
</td>
<td>
bool rewrite in one array per column, Implemented for ChunkedArray Array
is already contiguous. Not implemented for Table. C
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_from_arrow_:_schema">schema</code>
</td>
<td>
named list of DataTypes or char vec of names. Same length as arrow
table. If schema names or types do not match arrow table, the columns
will be renamed/recast. NULL default is to import columns as is. Takes
no effect for Array or ChunkedArray
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_from_arrow_:_schema_overrides">schema_overrides</code>
</td>
<td>
named list of DataTypes. Name some columns to recast by the DataType.
Takes not effect for Array or ChunkedArray
</td>
</tr>
</table>

## Value

DataFrame or Series

## Examples

``` r
library(polars)

pl$from_arrow(
  data = arrow::arrow_table(iris),
  schema_overrides = list(Sepal.Length = pl$Float32, Species = pl$Utf8)
)
```

    #> shape: (150, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       │
    #> │ f32          ┆ f64         ┆ f64          ┆ f64         ┆ str       │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa    │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa    │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …         │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         ┆ virginica │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         ┆ virginica │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┘

``` r
char_schema = names(iris)
char_schema[1] = "Alice"
pl$from_arrow(
  data = arrow::arrow_table(iris),
  schema = char_schema
)
```

    #> shape: (150, 5)
    #> ┌───────┬─────────────┬──────────────┬─────────────┬───────────┐
    #> │ Alice ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---   ┆ ---         ┆ ---          ┆ ---         ┆ ---       │
    #> │ f64   ┆ f64         ┆ f64          ┆ f64         ┆ cat       │
    #> ╞═══════╪═════════════╪══════════════╪═════════════╪═══════════╡
    #> │ 5.1   ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.9   ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.7   ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa    │
    #> │ 4.6   ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa    │
    #> │ …     ┆ …           ┆ …            ┆ …           ┆ …         │
    #> │ 6.3   ┆ 2.5         ┆ 5.0          ┆ 1.9         ┆ virginica │
    #> │ 6.5   ┆ 3.0         ┆ 5.2          ┆ 2.0         ┆ virginica │
    #> │ 6.2   ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica │
    #> │ 5.9   ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica │
    #> └───────┴─────────────┴──────────────┴─────────────┴───────────┘
