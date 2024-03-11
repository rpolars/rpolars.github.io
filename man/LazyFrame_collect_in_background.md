

# Collect a query in background

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L524)

## Description

This doesn’t block the R session as it calls
<code style="white-space: pre;">$collect()</code> in a a detached
thread. This can also be used via
<code style="white-space: pre;">$collect(collect_in_background =
TRUE)</code>.

## Usage

<pre><code class='language-R'>LazyFrame_collect_in_background()
</code></pre>

## Details

This function immediately returns an RThreadHandle. Use
<code>\<RPolarsRThreadHandle\>$is_finished()</code> to see if done. Use
<code>\<RPolarsRThreadHandle\>$join()</code> to wait and get the final
result.

It is useful to not block the R session while query executes. If you use
<code>\<Expr\>$map_batches()</code> or
<code>\<Expr\>$map_elements()</code> to run R functions in the query,
then you must pass <code>in_background = TRUE</code> in
<code>$map_batches()</code> (or <code>$map_elements()</code>).
Otherwise,
<code style="white-space: pre;">$collect_in_background()</code> will
fail because the main R session is not available for polars execution.
See also examples below.

## Value

RThreadHandle, a future-like thread handle for the task

## Examples

``` r
library(polars)

# Some expression which does contain a map
expr = pl$col("mpg")$map_batches(
  \(x) {
    Sys.sleep(.1)
    x * 0.43
  },
  in_background = TRUE # set TRUE if collecting in background queries with $map or $apply
)$alias("kml")

# return is immediately a handle to another thread.
handle = pl$LazyFrame(mtcars)$with_columns(expr)$collect_in_background()

# ask if query is done
if (!handle$is_finished()) print("not done yet")
```

    #> [1] "not done yet"

``` r
# get result, blocking until polars query is done
df = handle$join()
df
```

    #> shape: (32, 12)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬──────┬──────┬────────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ am  ┆ gear ┆ carb ┆ kml    │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ ---  ┆ ---  ┆ ---    │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64  ┆ f64  ┆ f64    │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪══════╪══════╪════════╡
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 4.0  ┆ 9.03   │
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 4.0  ┆ 9.03   │
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 4.0  ┆ 1.0  ┆ 9.804  │
    #> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 3.0  ┆ 1.0  ┆ 9.202  │
    #> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 3.0  ┆ 2.0  ┆ 8.041  │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …    ┆ …    ┆ …      │
    #> │ 30.4 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 2.0  ┆ 13.072 │
    #> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 4.0  ┆ 6.794  │
    #> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 6.0  ┆ 8.471  │
    #> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 1.0 ┆ 5.0  ┆ 8.0  ┆ 6.45   │
    #> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 4.0  ┆ 2.0  ┆ 9.202  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴──────┴──────┴────────┘
