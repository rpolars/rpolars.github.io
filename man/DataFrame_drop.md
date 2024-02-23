

# Drop columns of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/dataframe__frame.R#L420)

## Description

Drop columns of a DataFrame

## Usage

<pre><code class='language-R'>DataFrame_drop(columns)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_drop_:_columns">columns</code>
</td>
<td>
A character vector with the names of the column(s) to remove.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$drop(c("mpg", "hp"))
```

    #> shape: (32, 9)
    #> ┌─────┬───────┬──────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ cyl ┆ disp  ┆ drat ┆ wt    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ --- ┆ ---   ┆ ---  ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64 ┆ f64   ┆ f64  ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞═════╪═══════╪══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 6.0 ┆ 160.0 ┆ 3.9  ┆ 2.62  ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 6.0 ┆ 160.0 ┆ 3.9  ┆ 2.875 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 4.0 ┆ 108.0 ┆ 3.85 ┆ 2.32  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 6.0 ┆ 258.0 ┆ 3.08 ┆ 3.215 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ 8.0 ┆ 360.0 ┆ 3.15 ┆ 3.44  ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
    #> │ …   ┆ …     ┆ …    ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ 4.0 ┆ 95.1  ┆ 3.77 ┆ 1.513 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 2.0  │
    #> │ 8.0 ┆ 351.0 ┆ 4.22 ┆ 3.17  ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
    #> │ 6.0 ┆ 145.0 ┆ 3.62 ┆ 2.77  ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
    #> │ 8.0 ┆ 301.0 ┆ 3.54 ┆ 3.57  ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> │ 4.0 ┆ 121.0 ┆ 4.11 ┆ 2.78  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └─────┴───────┴──────┴───────┴───┴─────┴─────┴──────┴──────┘
