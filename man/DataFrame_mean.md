

# Mean

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1116)

## Description

Aggregate the columns in the DataFrame to their mean value.

## Usage

<pre><code class='language-R'>DataFrame_mean()
</code></pre>

## Value

A DataFrame with one row.

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$mean()
```

    #> shape: (1, 11)
    #> ┌───────────┬────────┬────────────┬──────────┬───┬────────┬─────────┬────────┬────────┐
    #> │ mpg       ┆ cyl    ┆ disp       ┆ hp       ┆ … ┆ vs     ┆ am      ┆ gear   ┆ carb   │
    #> │ ---       ┆ ---    ┆ ---        ┆ ---      ┆   ┆ ---    ┆ ---     ┆ ---    ┆ ---    │
    #> │ f64       ┆ f64    ┆ f64        ┆ f64      ┆   ┆ f64    ┆ f64     ┆ f64    ┆ f64    │
    #> ╞═══════════╪════════╪════════════╪══════════╪═══╪════════╪═════════╪════════╪════════╡
    #> │ 20.090625 ┆ 6.1875 ┆ 230.721875 ┆ 146.6875 ┆ … ┆ 0.4375 ┆ 0.40625 ┆ 3.6875 ┆ 2.8125 │
    #> └───────────┴────────┴────────────┴──────────┴───┴────────┴─────────┴────────┴────────┘
