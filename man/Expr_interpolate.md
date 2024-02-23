

# Interpolate null values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2343)

## Description

Fill nulls with linear interpolation using non-missing values. Can also
be used to regrid data to a new grid - see examples below.

## Usage

<pre><code class='language-R'>Expr_interpolate(method = "linear")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_interpolate_:_method">method</code>
</td>
<td>
String, either <code>“linear”</code> (default) or
<code>“nearest”</code>.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1, NA, 4, NA, 100, NaN, 150))$
  with_columns(
  interp_lin = pl$col("x")$interpolate(),
  interp_near = pl$col("x")$interpolate("nearest")
)
```

    #> shape: (7, 3)
    #> ┌───────┬────────────┬─────────────┐
    #> │ x     ┆ interp_lin ┆ interp_near │
    #> │ ---   ┆ ---        ┆ ---         │
    #> │ f64   ┆ f64        ┆ f64         │
    #> ╞═══════╪════════════╪═════════════╡
    #> │ 1.0   ┆ 1.0        ┆ 1.0         │
    #> │ null  ┆ 2.5        ┆ 4.0         │
    #> │ 4.0   ┆ 4.0        ┆ 4.0         │
    #> │ null  ┆ 52.0       ┆ 100.0       │
    #> │ 100.0 ┆ 100.0      ┆ 100.0       │
    #> │ NaN   ┆ NaN        ┆ NaN         │
    #> │ 150.0 ┆ 150.0      ┆ 150.0       │
    #> └───────┴────────────┴─────────────┘

``` r
# x, y interpolation over a grid
df_original_grid = pl$DataFrame(
  grid_points = c(1, 3, 10),
  values = c(2.0, 6.0, 20.0)
)
df_original_grid
```

    #> shape: (3, 2)
    #> ┌─────────────┬────────┐
    #> │ grid_points ┆ values │
    #> │ ---         ┆ ---    │
    #> │ f64         ┆ f64    │
    #> ╞═════════════╪════════╡
    #> │ 1.0         ┆ 2.0    │
    #> │ 3.0         ┆ 6.0    │
    #> │ 10.0        ┆ 20.0   │
    #> └─────────────┴────────┘

``` r
df_new_grid = pl$DataFrame(grid_points = (1:10) * 1.0)
df_new_grid
```

    #> shape: (10, 1)
    #> ┌─────────────┐
    #> │ grid_points │
    #> │ ---         │
    #> │ f64         │
    #> ╞═════════════╡
    #> │ 1.0         │
    #> │ 2.0         │
    #> │ 3.0         │
    #> │ 4.0         │
    #> │ 5.0         │
    #> │ 6.0         │
    #> │ 7.0         │
    #> │ 8.0         │
    #> │ 9.0         │
    #> │ 10.0        │
    #> └─────────────┘

``` r
# Interpolate from this to the new grid
df_new_grid$join(
  df_original_grid,
  on = "grid_points", how = "left"
)$with_columns(pl$col("values")$interpolate())
```

    #> shape: (10, 2)
    #> ┌─────────────┬────────┐
    #> │ grid_points ┆ values │
    #> │ ---         ┆ ---    │
    #> │ f64         ┆ f64    │
    #> ╞═════════════╪════════╡
    #> │ 1.0         ┆ 2.0    │
    #> │ 2.0         ┆ 4.0    │
    #> │ 3.0         ┆ 6.0    │
    #> │ 4.0         ┆ 8.0    │
    #> │ 5.0         ┆ 10.0   │
    #> │ 6.0         ┆ 12.0   │
    #> │ 7.0         ┆ 14.0   │
    #> │ 8.0         ┆ 16.0   │
    #> │ 9.0         ┆ 18.0   │
    #> │ 10.0        ┆ 20.0   │
    #> └─────────────┴────────┘
