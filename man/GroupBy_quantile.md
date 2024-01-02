
# Quantile

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/group_by.R#L250)

## Description

Aggregate the columns in the DataFrame to their quantile value.

## Usage

<pre><code class='language-R'>GroupBy_quantile(quantile, interpolation = "nearest")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="GroupBy_quantile_:_quantile">quantile</code>
</td>
<td>
numeric Quantile between 0.0 and 1.0.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="GroupBy_quantile_:_interpolation">interpolation</code>
</td>
<td>
string Interpolation method: "nearest", "higher", "lower", "midpoint",
or "linear".
</td>
</tr>
</table>

## Value

GroupBy

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$lazy()$quantile(.4)$collect()
```

    #> shape: (1, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 17.8 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
