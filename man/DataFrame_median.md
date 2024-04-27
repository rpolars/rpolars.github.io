

# Median

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/dataframe__frame.R#L1270)

## Description

Aggregate the columns in the DataFrame to their median value.

## Usage

<pre><code class='language-R'>DataFrame_median()
</code></pre>

## Value

A DataFrame with one row.

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$median()
```

    #> shape: (1, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 19.2 ┆ 6.0 ┆ 196.3 ┆ 123.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 4.0  ┆ 2.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
