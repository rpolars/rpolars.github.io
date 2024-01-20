
# The RPolarsRThreadHandle class

## Description

A handle to some polars query running in a background thread.

## Details

<code>\<LazyFrame\>$collect_in_background()</code> will execute a polars
query detached from the R session and return an
<code>RPolarsRThreadHandle</code> immediately. This
<code>RPolarsRThreadHandle</code>-class has the methods
<code>is_finished()</code> and <code>join()</code>.

NOTICE: The background thread cannot use the main R session, but can
access the pool of extra R sessions to process R code embedded in polars
query via <code>$map_batches(…, in_background = TRUE)</code> or
<code style="white-space: pre;">$map_elements(background=TRUE)</code>.
Use <code>pl$set_options(rpool_cap = XX)</code> to limit number of
parallel R sessions. Starting polars
<code>\<LazyFrame\>$collect_in_background()</code> with e.g. some
<code>$map_batches(…, in_background = FALSE)</code> will raise an Error
as the main R session is not available to process the R part of the
polars query. Native polars query does not need any R session.

## Value

see methods: <code>is_finished()</code> <code>join()</code>

## See Also

<code>\<LazyFrame\>$collect_in_background()</code>
<code>\<Expr\>$map_batches()</code> <code>\<Expr\>$map_elements()</code>

## Examples

``` r
library(polars)

prexpr = pl$col("mpg")$map_batches(\(x) {
  Sys.sleep(.1)
  x * 0.43
}, in_background = TRUE)$alias("kml")
handle = pl$LazyFrame(mtcars)$with_columns(prexpr)$collect_in_background()
if (!handle$is_finished()) print("not done yet")
```

    #> [1] "not done yet"

``` r
df = handle$join() # get result
df
```

    #> shape: (32, 12)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬──────┬──────┬───────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ am  ┆ gear ┆ carb ┆ kml   │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ ---  ┆ ---  ┆ ---   │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64  ┆ f64  ┆ f64   │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪══════╪══════╪═══════╡
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 4.0  ┆ 9.03  │
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 4.0  ┆ 9.03  │
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 4.0  ┆ 1.0  ┆ 9.804 │
    #> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 3.0  ┆ 1.0  ┆ 9.202 │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …    ┆ …    ┆ …     │
    #> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 4.0  ┆ 6.794 │
    #> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 6.0  ┆ 8.471 │
    #> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 8.0  ┆ 6.45  │
    #> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 2.0  ┆ 9.202 │
    #> └──────┴─────┴───────┴───────┴───┴─────┴──────┴──────┴───────┘
