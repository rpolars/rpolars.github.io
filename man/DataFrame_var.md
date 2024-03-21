

# Var

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1237)

## Description

Aggregate the columns of this DataFrame to their variance values.

## Usage

<pre><code class='language-R'>DataFrame_var(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_var_:_ddof">ddof</code>
</td>
<td>
Delta Degrees of Freedom: the divisor used in the calculation is N -
ddof, where N represents the number of elements. By default ddof is 1.
</td>
</tr>
</table>

## Value

A DataFrame with one row.

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$var()
```

    #> shape: (1, 11)
    #> ┌───────────┬──────────┬─────────────┬─────────────┬───┬──────────┬──────────┬──────────┬──────────┐
    #> │ mpg       ┆ cyl      ┆ disp        ┆ hp          ┆ … ┆ vs       ┆ am       ┆ gear     ┆ carb     │
    #> │ ---       ┆ ---      ┆ ---         ┆ ---         ┆   ┆ ---      ┆ ---      ┆ ---      ┆ ---      │
    #> │ f64       ┆ f64      ┆ f64         ┆ f64         ┆   ┆ f64      ┆ f64      ┆ f64      ┆ f64      │
    #> ╞═══════════╪══════════╪═════════════╪═════════════╪═══╪══════════╪══════════╪══════════╪══════════╡
    #> │ 36.324103 ┆ 3.189516 ┆ 15360.79982 ┆ 4700.866935 ┆ … ┆ 0.254032 ┆ 0.248992 ┆ 0.544355 ┆ 2.608871 │
    #> │           ┆          ┆ 9           ┆             ┆   ┆          ┆          ┆          ┆          │
    #> └───────────┴──────────┴─────────────┴─────────────┴───┴──────────┴──────────┴──────────┴──────────┘
