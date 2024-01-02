
# Count null values

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/#L)

## Description

Create a new DataFrame that shows the null (which correspond to
<code>NA</code> in R) counts per column.

## Usage

<pre><code class='language-R'>DataFrame_null_count
</code></pre>

## Format

function

## Value

DataFrame

## Examples

``` r
library(polars)

x = mtcars
x[1, 2:3] = NA
pl$DataFrame(x)$null_count()
```

    #> shape: (1, 11)
    #> ┌─────┬─────┬──────┬─────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg ┆ cyl ┆ disp ┆ hp  ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ --- ┆ --- ┆ ---  ┆ --- ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ u32 ┆ u32 ┆ u32  ┆ u32 ┆   ┆ u32 ┆ u32 ┆ u32  ┆ u32  │
    #> ╞═════╪═════╪══════╪═════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 0   ┆ 1   ┆ 1    ┆ 0   ┆ … ┆ 0   ┆ 0   ┆ 0    ┆ 0    │
    #> └─────┴─────┴──────┴─────┴───┴─────┴─────┴──────┴──────┘
