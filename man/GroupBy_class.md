

# Operations on Polars grouped DataFrame

## Description

The GroupBy class in R, is just another interface on top of the
DataFrame in rust polars. Groupby does not use the rust api for
<code>\<DataFrame\>$group_by()</code> + <code>$agg()</code> because the
groupby-struct is a reference to a DataFrame and that reference will
share lifetime with its parent DataFrame.

## Details

There is no way to expose lifetime limited objects via extendr currently
(might be quirky anyhow with R GC). Instead the inputs for the
<code>group_by</code> are just stored on R side, until also
<code>agg</code> is called. Which will end up in a self-owned DataFrame
object and all is fine. groupby aggs are performed via the rust polars
LazyGroupBy methods, see DataFrame.groupby_agg method.

## Active bindings

<h4>
columns
</h4>

<code style="white-space: pre;">$columns</code> returns a character
vector with the column names.

## Examples

``` r
library(polars)

as_polars_df(mtcars)$group_by("cyl")$agg(
  pl$col("mpg")$sum()
)
```

    #> shape: (3, 2)
    #> ┌─────┬───────┐
    #> │ cyl ┆ mpg   │
    #> │ --- ┆ ---   │
    #> │ f64 ┆ f64   │
    #> ╞═════╪═══════╡
    #> │ 8.0 ┆ 211.4 │
    #> │ 6.0 ┆ 138.2 │
    #> │ 4.0 ┆ 293.3 │
    #> └─────┴───────┘
