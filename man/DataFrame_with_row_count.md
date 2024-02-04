

# Add a column for row indices

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/dataframe__frame.R#L315)

## Description

Add a new column at index 0 that counts the rows

## Usage

<pre><code class='language-R'>DataFrame_with_row_count(name, offset = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_with_row_count_:_name">name</code>
</td>
<td>
string name of the created column
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_with_row_count_:_offset">offset</code>
</td>
<td>
positive integer offset for the start of the counter
</td>
</tr>
</table>

## Value

A new <code>DataFrame</code> object with a counter column in front

## Examples

``` r
library(polars)

df = pl$DataFrame(mtcars)

# by default, the index starts at 0 (to mimic the behavior of Python Polars)
df$with_row_count("idx")
```

    #> shape: (32, 12)
    #> ┌─────┬──────┬─────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ idx ┆ mpg  ┆ cyl ┆ disp  ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ --- ┆ ---  ┆ --- ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ u32 ┆ f64  ┆ f64 ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞═════╪══════╪═════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 0   ┆ 21.0 ┆ 6.0 ┆ 160.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 1   ┆ 21.0 ┆ 6.0 ┆ 160.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 2   ┆ 22.8 ┆ 4.0 ┆ 108.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 3   ┆ 21.4 ┆ 6.0 ┆ 258.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ …   ┆ …    ┆ …   ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ 28  ┆ 15.8 ┆ 8.0 ┆ 351.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
    #> │ 29  ┆ 19.7 ┆ 6.0 ┆ 145.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
    #> │ 30  ┆ 15.0 ┆ 8.0 ┆ 301.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> │ 31  ┆ 21.4 ┆ 4.0 ┆ 121.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └─────┴──────┴─────┴───────┴───┴─────┴─────┴──────┴──────┘

``` r
# but in R, we use a 1-index
df$with_row_count("idx", offset = 1)
```

    #> shape: (32, 12)
    #> ┌─────┬──────┬─────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ idx ┆ mpg  ┆ cyl ┆ disp  ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ --- ┆ ---  ┆ --- ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ u32 ┆ f64  ┆ f64 ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞═════╪══════╪═════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 1   ┆ 21.0 ┆ 6.0 ┆ 160.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 2   ┆ 21.0 ┆ 6.0 ┆ 160.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 3   ┆ 22.8 ┆ 4.0 ┆ 108.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 4   ┆ 21.4 ┆ 6.0 ┆ 258.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ …   ┆ …    ┆ …   ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ 29  ┆ 15.8 ┆ 8.0 ┆ 351.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
    #> │ 30  ┆ 19.7 ┆ 6.0 ┆ 145.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
    #> │ 31  ┆ 15.0 ┆ 8.0 ┆ 301.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> │ 32  ┆ 21.4 ┆ 4.0 ┆ 121.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └─────┴──────┴─────┴───────┴───┴─────┴─────┴──────┴──────┘
