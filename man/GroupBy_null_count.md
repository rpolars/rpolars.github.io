

# GroupBy null count

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/group_by.R#L304)

## Description

Create a new DataFrame that shows the null counts per column.

## Usage

<pre><code class='language-R'>GroupBy_null_count()
</code></pre>

## Value

DataFrame

## Examples

``` r
library(polars)

x = mtcars
x[1:10, 3:5] = NA
pl$DataFrame(x)$group_by("cyl")$null_count()
```

    #> shape: (3, 11)
    #> ┌─────┬─────┬──────┬─────┬───┬─────┬─────┬──────┬──────┐
    #> │ cyl ┆ mpg ┆ disp ┆ hp  ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ --- ┆ --- ┆ ---  ┆ --- ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64 ┆ u32 ┆ u32  ┆ u32 ┆   ┆ u32 ┆ u32 ┆ u32  ┆ u32  │
    #> ╞═════╪═════╪══════╪═════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 6.0 ┆ 0   ┆ 5    ┆ 5   ┆ … ┆ 0   ┆ 0   ┆ 0    ┆ 0    │
    #> │ 8.0 ┆ 0   ┆ 2    ┆ 2   ┆ … ┆ 0   ┆ 0   ┆ 0    ┆ 0    │
    #> │ 4.0 ┆ 0   ┆ 3    ┆ 3   ┆ … ┆ 0   ┆ 0   ┆ 0    ┆ 0    │
    #> └─────┴─────┴──────┴─────┴───┴─────┴─────┴──────┴──────┘
