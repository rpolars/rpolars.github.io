

# Map an expression with an R function

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L804)

## Description

Map an expression with an R function

## Usage

<pre><code class='language-R'>Expr_map_batches(
  f,
  output_type = NULL,
  agg_list = FALSE,
  in_background = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_map_batches_:_f">f</code>
</td>
<td>
a function to map with
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_map_batches_:_output_type">output_type</code>
</td>
<td>
<code>NULL</code> or a type available in <code>names(pl$dtypes)</code>.
If <code>NULL</code> (default), the output datatype will match the input
datatype. This is used to inform schema of the actual return type of the
R function. Setting this wrong could theoretically have some downstream
implications to the query.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_map_batches_:_agg_list">agg_list</code>
</td>
<td>
Aggregate list. Map from vector to group in group_by context.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_map_batches_:_in_background">in_background</code>
</td>
<td>
Boolean. Whether to execute the map in a background R process. Combined
with setting e.g. <code>options(polars.rpool_cap = 4)</code> it can
speed up some slow R functions as they can run in parallel R sessions.
The communication speed between processes is quite slower than between
threads. This will likely only give a speed-up in a "low IO - high CPU"
use case. If there are multiple <code>$map_batches(in_background =
TRUE)</code> calls in the query, they will be run in parallel.
</td>
</tr>
</table>

## Details

It is sometimes necessary to apply a specific R function on one or
several columns. However, note that using R code in
<code>$map_batches()</code> is slower than native polars. The user
function must take one polars <code>Series</code> as input and the
return should be a <code>Series</code> or any Robj convertible into a
<code>Series</code> (e.g. vectors). Map fully supports
<code>browser()</code>.

If <code>in_background = FALSE</code> the function can access any global
variable of the R session. However, note that several calls to
<code>$map_batches()</code> will sequentially share the same main R
session, so the global environment might change between the start of the
query and the moment a <code>$map_batches()</code> call is evaluated.
Any native polars computations can still be executed meanwhile. If
<code>in_background = TRUE</code>, the map will run in one or more other
R sessions and will not have access to global variables. Use
<code>options(polars.rpool_cap = 4)</code> and
<code>polars_options()$rpool_cap</code> to set and view number of
parallel R sessions.

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(iris)$
  select(
  pl$col("Sepal.Length")$map_batches(\(x) {
    paste("cheese", as.character(x$to_vector()))
  }, pl$dtypes$String)
)
```

    #> shape: (150, 1)
    #> ┌──────────────┐
    #> │ Sepal.Length │
    #> │ ---          │
    #> │ str          │
    #> ╞══════════════╡
    #> │ cheese 5.1   │
    #> │ cheese 4.9   │
    #> │ cheese 4.7   │
    #> │ cheese 4.6   │
    #> │ cheese 5     │
    #> │ …            │
    #> │ cheese 6.7   │
    #> │ cheese 6.3   │
    #> │ cheese 6.5   │
    #> │ cheese 6.2   │
    #> │ cheese 5.9   │
    #> └──────────────┘

``` r
# R parallel process example, use Sys.sleep() to imitate some CPU expensive
# computation.

# map a,b,c,d sequentially
pl$LazyFrame(a = 1, b = 2, c = 3, d = 4)$select(
  pl$all()$map_batches(\(s) {
    Sys.sleep(.1)
    s * 2
  })
)$collect() |> system.time()
```

    #>    user  system elapsed 
    #>   0.028   0.000   0.428

``` r
# map in parallel 1: Overhead to start up extra R processes / sessions
options(polars.rpool_cap = 0) # drop any previous processes, just to show start-up overhead
options(polars.rpool_cap = 4) # set back to 4, the default
polars_options()$rpool_cap
```

    #> [1] 4

``` r
pl$LazyFrame(a = 1, b = 2, c = 3, d = 4)$select(
  pl$all()$map_batches(\(s) {
    Sys.sleep(.1)
    s * 2
  }, in_background = TRUE)
)$collect() |> system.time()
```

    #>    user  system elapsed 
    #>   0.009   0.001   0.978

``` r
# map in parallel 2: Reuse R processes in "polars global_rpool".
polars_options()$rpool_cap
```

    #> [1] 4

``` r
pl$LazyFrame(a = 1, b = 2, c = 3, d = 4)$select(
  pl$all()$map_batches(\(s) {
    Sys.sleep(.1)
    s * 2
  }, in_background = TRUE)
)$collect() |> system.time()
```

    #>    user  system elapsed 
    #>   0.003   0.007   0.122
