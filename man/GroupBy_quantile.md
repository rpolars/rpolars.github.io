

# Quantile

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/group_by.R#L271)

## Description

Aggregate the columns in the DataFrame to their quantile value.

## Usage

<pre><code class='language-R'>GroupBy_quantile(quantile, interpolation = "nearest")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="quantile">quantile</code>
</td>
<td>
numeric Quantile between 0.0 and 1.0.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="interpolation">interpolation</code>
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
