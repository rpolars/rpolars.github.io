

# Shift a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L751)

## Description

Shift the values by a given period. If the period (<code>n</code>) is
positive, then <code>n</code> rows will be inserted at the top of the
DataFrame and the last <code>n</code> rows will be discarded. Vice-versa
if the period is negative. In the end, the total number of rows of the
DataFrame doesn’t change.

## Usage

<pre><code class='language-R'>DataFrame_shift(periods = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_shift_:_periods">periods</code>
</td>
<td>
Number of periods to shift (can be negative).
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$shift(2)
```

    #> shape: (32, 11)
    #> ┌──────┬──────┬───────┬───────┬───┬──────┬──────┬──────┬──────┐
    #> │ mpg  ┆ cyl  ┆ disp  ┆ hp    ┆ … ┆ vs   ┆ am   ┆ gear ┆ carb │
    #> │ ---  ┆ ---  ┆ ---   ┆ ---   ┆   ┆ ---  ┆ ---  ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64  ┆ f64   ┆ f64   ┆   ┆ f64  ┆ f64  ┆ f64  ┆ f64  │
    #> ╞══════╪══════╪═══════╪═══════╪═══╪══════╪══════╪══════╪══════╡
    #> │ null ┆ null ┆ null  ┆ null  ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ null ┆ null ┆ null  ┆ null  ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ 21.0 ┆ 6.0  ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 4.0  ┆ 4.0  │
    #> │ 21.0 ┆ 6.0  ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 4.0  ┆ 4.0  │
    #> │ 22.8 ┆ 4.0  ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0  ┆ 1.0  ┆ 4.0  ┆ 1.0  │
    #> │ …    ┆ …    ┆ …     ┆ …     ┆ … ┆ …    ┆ …    ┆ …    ┆ …    │
    #> │ 27.3 ┆ 4.0  ┆ 79.0  ┆ 66.0  ┆ … ┆ 1.0  ┆ 1.0  ┆ 4.0  ┆ 1.0  │
    #> │ 26.0 ┆ 4.0  ┆ 120.3 ┆ 91.0  ┆ … ┆ 0.0  ┆ 1.0  ┆ 5.0  ┆ 2.0  │
    #> │ 30.4 ┆ 4.0  ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0  ┆ 1.0  ┆ 5.0  ┆ 2.0  │
    #> │ 15.8 ┆ 8.0  ┆ 351.0 ┆ 264.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 5.0  ┆ 4.0  │
    #> │ 19.7 ┆ 6.0  ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 5.0  ┆ 6.0  │
    #> └──────┴──────┴───────┴───────┴───┴──────┴──────┴──────┴──────┘

``` r
pl$DataFrame(mtcars)$shift(-2)
```

    #> shape: (32, 11)
    #> ┌──────┬──────┬───────┬───────┬───┬──────┬──────┬──────┬──────┐
    #> │ mpg  ┆ cyl  ┆ disp  ┆ hp    ┆ … ┆ vs   ┆ am   ┆ gear ┆ carb │
    #> │ ---  ┆ ---  ┆ ---   ┆ ---   ┆   ┆ ---  ┆ ---  ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64  ┆ f64   ┆ f64   ┆   ┆ f64  ┆ f64  ┆ f64  ┆ f64  │
    #> ╞══════╪══════╪═══════╪═══════╪═══╪══════╪══════╪══════╪══════╡
    #> │ 22.8 ┆ 4.0  ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0  ┆ 1.0  ┆ 4.0  ┆ 1.0  │
    #> │ 21.4 ┆ 6.0  ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0  ┆ 0.0  ┆ 3.0  ┆ 1.0  │
    #> │ 18.7 ┆ 8.0  ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0  ┆ 0.0  ┆ 3.0  ┆ 2.0  │
    #> │ 18.1 ┆ 6.0  ┆ 225.0 ┆ 105.0 ┆ … ┆ 1.0  ┆ 0.0  ┆ 3.0  ┆ 1.0  │
    #> │ 14.3 ┆ 8.0  ┆ 360.0 ┆ 245.0 ┆ … ┆ 0.0  ┆ 0.0  ┆ 3.0  ┆ 4.0  │
    #> │ …    ┆ …    ┆ …     ┆ …     ┆ … ┆ …    ┆ …    ┆ …    ┆ …    │
    #> │ 19.7 ┆ 6.0  ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 5.0  ┆ 6.0  │
    #> │ 15.0 ┆ 8.0  ┆ 301.0 ┆ 335.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 5.0  ┆ 8.0  │
    #> │ 21.4 ┆ 4.0  ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0  ┆ 1.0  ┆ 4.0  ┆ 2.0  │
    #> │ null ┆ null ┆ null  ┆ null  ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ null ┆ null ┆ null  ┆ null  ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> └──────┴──────┴───────┴───────┴───┴──────┴──────┴──────┴──────┘
