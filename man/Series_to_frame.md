

# Convert Series to DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/series__series.R#L944)

## Description

Convert Series to DataFrame

## Usage

<pre><code class='language-R'>Series_to_frame()
</code></pre>

## Value

DataFrame

## Examples

``` r
library(polars)

# default will be a DataFrame with empty name
as_polars_series(1:4)$to_frame()
```

    #> shape: (4, 1)
    #> ┌─────┐
    #> │     │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> │ 4   │
    #> └─────┘

``` r
as_polars_series(1:4, "bob")$to_frame()
```

    #> shape: (4, 1)
    #> ┌─────┐
    #> │ bob │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> │ 4   │
    #> └─────┘
