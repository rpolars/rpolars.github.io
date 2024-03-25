

# Transpose a DataFrame over the diagonal.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1826)

## Description

Transpose a DataFrame over the diagonal.

## Usage

<pre><code class='language-R'>DataFrame_transpose(
  include_header = FALSE,
  header_name = "column",
  column_names = NULL
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_transpose_:_include_header">include_header</code>
</td>
<td>
If <code>TRUE</code>, the column names will be added as first column.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_transpose_:_header_name">header_name</code>
</td>
<td>
If <code>include_header</code> is <code>TRUE</code>, this determines the
name of the column that will be inserted.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_transpose_:_column_names">column_names</code>
</td>
<td>
Character vector indicating the new column names. If <code>NULL</code>
(default), the columns will be named as "column_1", "column_2", etc. The
length of this vector must match the number of rows of the original
input.
</td>
</tr>
</table>

## Details

This is a very expensive operation.

Transpose may be the fastest option to perform non foldable (see
<code>fold()</code> or <code>reduce()</code>) row operations like
median.

Polars transpose is currently eager only, likely because it is not
trivial to deduce the schema.

## Value

DataFrame

## Examples

``` r
library(polars)


# simple use-case
pl$DataFrame(mtcars)$transpose(include_header = TRUE, column_names = rownames(mtcars))
```

    #> shape: (11, 33)
    #> ┌────────┬───────────┬─────────────┬────────┬───┬─────────────┬─────────┬─────────────┬────────────┐
    #> │ column ┆ Mazda RX4 ┆ Mazda RX4   ┆ Datsun ┆ … ┆ Ford        ┆ Ferrari ┆ Maserati    ┆ Volvo 142E │
    #> │ ---    ┆ ---       ┆ Wag         ┆ 710    ┆   ┆ Pantera L   ┆ Dino    ┆ Bora        ┆ ---        │
    #> │ str    ┆ f64       ┆ ---         ┆ ---    ┆   ┆ ---         ┆ ---     ┆ ---         ┆ f64        │
    #> │        ┆           ┆ f64         ┆ f64    ┆   ┆ f64         ┆ f64     ┆ f64         ┆            │
    #> ╞════════╪═══════════╪═════════════╪════════╪═══╪═════════════╪═════════╪═════════════╪════════════╡
    #> │ mpg    ┆ 21.0      ┆ 21.0        ┆ 22.8   ┆ … ┆ 15.8        ┆ 19.7    ┆ 15.0        ┆ 21.4       │
    #> │ cyl    ┆ 6.0       ┆ 6.0         ┆ 4.0    ┆ … ┆ 8.0         ┆ 6.0     ┆ 8.0         ┆ 4.0        │
    #> │ disp   ┆ 160.0     ┆ 160.0       ┆ 108.0  ┆ … ┆ 351.0       ┆ 145.0   ┆ 301.0       ┆ 121.0      │
    #> │ hp     ┆ 110.0     ┆ 110.0       ┆ 93.0   ┆ … ┆ 264.0       ┆ 175.0   ┆ 335.0       ┆ 109.0      │
    #> │ drat   ┆ 3.9       ┆ 3.9         ┆ 3.85   ┆ … ┆ 4.22        ┆ 3.62    ┆ 3.54        ┆ 4.11       │
    #> │ …      ┆ …         ┆ …           ┆ …      ┆ … ┆ …           ┆ …       ┆ …           ┆ …          │
    #> │ qsec   ┆ 16.46     ┆ 17.02       ┆ 18.61  ┆ … ┆ 14.5        ┆ 15.5    ┆ 14.6        ┆ 18.6       │
    #> │ vs     ┆ 0.0       ┆ 0.0         ┆ 1.0    ┆ … ┆ 0.0         ┆ 0.0     ┆ 0.0         ┆ 1.0        │
    #> │ am     ┆ 1.0       ┆ 1.0         ┆ 1.0    ┆ … ┆ 1.0         ┆ 1.0     ┆ 1.0         ┆ 1.0        │
    #> │ gear   ┆ 4.0       ┆ 4.0         ┆ 4.0    ┆ … ┆ 5.0         ┆ 5.0     ┆ 5.0         ┆ 4.0        │
    #> │ carb   ┆ 4.0       ┆ 4.0         ┆ 1.0    ┆ … ┆ 4.0         ┆ 6.0     ┆ 8.0         ┆ 2.0        │
    #> └────────┴───────────┴─────────────┴────────┴───┴─────────────┴─────────┴─────────────┴────────────┘

``` r
# All rows must have one shared supertype, recast Categorical to String which is a supertype
# of f64, and then dataset "Iris" can be transposed
pl$DataFrame(iris)$with_columns(pl$col("Species")$cast(pl$String))$transpose()
```

    #> shape: (5, 150)
    #> ┌──────────┬──────────┬──────────┬──────────┬───┬────────────┬────────────┬────────────┬───────────┐
    #> │ column_0 ┆ column_1 ┆ column_2 ┆ column_3 ┆ … ┆ column_146 ┆ column_147 ┆ column_148 ┆ column_14 │
    #> │ ---      ┆ ---      ┆ ---      ┆ ---      ┆   ┆ ---        ┆ ---        ┆ ---        ┆ 9         │
    #> │ str      ┆ str      ┆ str      ┆ str      ┆   ┆ str        ┆ str        ┆ str        ┆ ---       │
    #> │          ┆          ┆          ┆          ┆   ┆            ┆            ┆            ┆ str       │
    #> ╞══════════╪══════════╪══════════╪══════════╪═══╪════════════╪════════════╪════════════╪═══════════╡
    #> │ 5.1      ┆ 4.9      ┆ 4.7      ┆ 4.6      ┆ … ┆ 6.3        ┆ 6.5        ┆ 6.2        ┆ 5.9       │
    #> │ 3.5      ┆ 3.0      ┆ 3.2      ┆ 3.1      ┆ … ┆ 2.5        ┆ 3.0        ┆ 3.4        ┆ 3.0       │
    #> │ 1.4      ┆ 1.4      ┆ 1.3      ┆ 1.5      ┆ … ┆ 5.0        ┆ 5.2        ┆ 5.4        ┆ 5.1       │
    #> │ 0.2      ┆ 0.2      ┆ 0.2      ┆ 0.2      ┆ … ┆ 1.9        ┆ 2.0        ┆ 2.3        ┆ 1.8       │
    #> │ setosa   ┆ setosa   ┆ setosa   ┆ setosa   ┆ … ┆ virginica  ┆ virginica  ┆ virginica  ┆ virginica │
    #> └──────────┴──────────┴──────────┴──────────┴───┴────────────┴────────────┴────────────┴───────────┘
