

# Min

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/dataframe__frame.R#L1148)

## Description

Aggregate the columns in the DataFrame to their minimum value.

## Usage

<pre><code class='language-R'>DataFrame_min()
</code></pre>

## Value

A DataFrame with one row.

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$min()
```

    #> shape: (1, 11)
    #> ┌──────┬─────┬──────┬──────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp ┆ hp   ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---  ┆ ---  ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64  ┆ f64  ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪══════╪══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 10.4 ┆ 4.0 ┆ 71.1 ┆ 52.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> └──────┴─────┴──────┴──────┴───┴─────┴─────┴──────┴──────┘
