

# Register multiple data as tables

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/sql.R#L110)

## Description

Register multiple frames as tables.

## Usage

<pre><code class='language-R'>SQLContext_register_many(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Name-value pairs of LazyFrame like objects to register.
</td>
</tr>
</table>

## Value

Returns the SQLContext_class object invisibly.

## Examples

``` r
library(polars)


ctx = pl$SQLContext()
r_df = mtcars
pl_df = pl$DataFrame(mtcars)
pl_lf = pl$LazyFrame(mtcars)

ctx$register_many(r_df = r_df, pl_df = pl_df, pl_lf = pl_lf)

ctx$execute(
  "SELECT * FROM r_df
  UNION ALL
  SELECT * FROM pl_df
  UNION ALL
  SELECT * FROM pl_lf"
)$collect()
```

    #> shape: (96, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ 30.4 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 2.0  │
    #> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
    #> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
    #> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
