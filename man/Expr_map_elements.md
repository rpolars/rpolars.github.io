

# Map a custom/user-defined function (UDF) to each element of a column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L897)

## Description

The UDF is applied to each element of a column. See Details for more
information on specificities related to the context.

## Usage

<pre><code class='language-R'>Expr_map_elements(
  f,
  return_type = NULL,
  strict_return_type = TRUE,
  allow_fail_eval = FALSE,
  in_background = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_map_elements_:_f">f</code>
</td>
<td>
Function to map
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_map_elements_:_return_type">return_type</code>
</td>
<td>
DataType of the output Series. If <code>NULL</code>, the dtype will be
<code>pl$Unknown</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_map_elements_:_strict_return_type">strict_return_type</code>
</td>
<td>
If <code>TRUE</code> (default), error if not correct datatype returned
from R. If <code>FALSE</code>, the output will be converted to a polars
null value.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_map_elements_:_allow_fail_eval">allow_fail_eval</code>
</td>
<td>
If <code>FALSE</code> (default), raise an error if the function fails.
If <code>TRUE</code>, the result will be converted to a polars null
value.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_map_elements_:_in_background">in_background</code>
</td>
<td>
Whether to run the function in a background R process, default is
<code>FALSE</code>. Combined with setting
e.g. <code>options(polars.rpool_cap = 4)</code>, this can speed up some
slow R functions as they can run in parallel R sessions. The
communication speed between processes is quite slower than between
threads. This will likely only give a speed-up in a "low IO - high CPU"
usecase. A single map will not be paralleled, only in case of multiple
<code style="white-space: pre;">$map_elements()</code> in the query can
these run in parallel.
</td>
</tr>
</table>

## Details

Note that, in a GroupBy context, the column will have been
pre-aggregated and so each element will itself be a Series. Therefore,
depending on the context, requirements for function differ:

<ul>
<li>

in <code style="white-space: pre;">$select()</code> or
<code style="white-space: pre;">$with_columns()</code> (selection
context), the function must operate on R values of length 1. Polars will
convert each element into an R value and pass it to the function. The
output of the user function will be converted back into a polars type
(the return type must match, see argument <code>return_type</code>).
Using <code style="white-space: pre;">$map_elements()</code> in this
context should be avoided as a <code>lapply()</code> has half the
overhead.

</li>
<li>

in <code style="white-space: pre;">$agg()</code> (GroupBy context), the
function must take a <code>Series</code> and return a
<code>Series</code> or an R object convertible to <code>Series</code>,
e.g. a vector. In this context, it is much faster if there are the
number of groups is much lower than the number of rows, as the iteration
is only across the groups. The R user function could e.g. convert the
<code>Series</code> to a vector with
<code style="white-space: pre;">$to_r()</code> and perform some
vectorized operations.

</li>
</ul>

Note that it is preferred to express your function in polars syntax,
which will almost always be <em>significantly</em> faster and more
memory efficient because:

<ul>
<li>

the native expression engine runs in Rust; functions run in R.

</li>
<li>

use of R functions forces the DataFrame to be materialized in memory.

</li>
<li>

Polars-native expressions can be parallelized (R functions cannot).

</li>
<li>

Polars-native expressions can be logically optimized (R functions
cannot).

</li>
</ul>

Wherever possible you should strongly prefer the native expression API
to achieve the best performance and avoid using
<code style="white-space: pre;">$map_elements()</code>.

## Value

Expr

## Examples

``` r
library(polars)

# apply over groups: here, the input must be a Series
# prepare two expressions, one to compute the sum of each variable, one to
# get the first two values of each variable and store them in a list
e_sum = pl$all()$map_elements(\(s) sum(s$to_r()))$name$suffix("_sum")
e_head = pl$all()$map_elements(\(s) head(s$to_r(), 2))$name$suffix("_head")
pl$DataFrame(iris)$group_by("Species")$agg(e_sum, e_head)
```

    #> shape: (3, 9)
    #> ┌───────────┬───────────┬───────────┬───────────┬───┬───────────┬───────────┬───────────┬──────────┐
    #> │ Species   ┆ Sepal.Len ┆ Sepal.Wid ┆ Petal.Len ┆ … ┆ Sepal.Len ┆ Sepal.Wid ┆ Petal.Len ┆ Petal.Wi │
    #> │ ---       ┆ gth_sum   ┆ th_sum    ┆ gth_sum   ┆   ┆ gth_head  ┆ th_head   ┆ gth_head  ┆ dth_head │
    #> │ cat       ┆ ---       ┆ ---       ┆ ---       ┆   ┆ ---       ┆ ---       ┆ ---       ┆ ---      │
    #> │           ┆ f64       ┆ f64       ┆ f64       ┆   ┆ list[f64] ┆ list[f64] ┆ list[f64] ┆ list[f64 │
    #> │           ┆           ┆           ┆           ┆   ┆           ┆           ┆           ┆ ]        │
    #> ╞═══════════╪═══════════╪═══════════╪═══════════╪═══╪═══════════╪═══════════╪═══════════╪══════════╡
    #> │ virginica ┆ 329.4     ┆ 148.7     ┆ 277.6     ┆ … ┆ [6.3,     ┆ [3.3,     ┆ [6.0,     ┆ [2.5,    │
    #> │           ┆           ┆           ┆           ┆   ┆ 5.8]      ┆ 2.7]      ┆ 5.1]      ┆ 1.9]     │
    #> │ setosa    ┆ 250.3     ┆ 171.4     ┆ 73.1      ┆ … ┆ [5.1,     ┆ [3.5,     ┆ [1.4,     ┆ [0.2,    │
    #> │           ┆           ┆           ┆           ┆   ┆ 4.9]      ┆ 3.0]      ┆ 1.4]      ┆ 0.2]     │
    #> │ versicolo ┆ 296.8     ┆ 138.5     ┆ 213.0     ┆ … ┆ [7.0,     ┆ [3.2,     ┆ [4.7,     ┆ [1.4,    │
    #> │ r         ┆           ┆           ┆           ┆   ┆ 6.4]      ┆ 3.2]      ┆ 4.5]      ┆ 1.5]     │
    #> └───────────┴───────────┴───────────┴───────────┴───┴───────────┴───────────┴───────────┴──────────┘

``` r
# apply a function on each value (should be avoided): here the input is an R
# value of length 1
# select only Float64 columns
my_selection = pl$col(pl$dtypes$Float64)

# prepare two expressions, the first one only adds 10 to each element, the
# second returns the letter whose index matches the element
e_add10 = my_selection$map_elements(\(x)  {
  x + 10
})$name$suffix("_sum")

e_letter = my_selection$map_elements(\(x) {
  letters[ceiling(x)]
}, return_type = pl$dtypes$String)$name$suffix("_letter")
pl$DataFrame(iris)$select(e_add10, e_letter)
```

    #> shape: (150, 8)
    #> ┌────────────┬────────────┬────────────┬───────────┬───────────┬───────────┬───────────┬───────────┐
    #> │ Sepal.Leng ┆ Sepal.Widt ┆ Petal.Leng ┆ Petal.Wid ┆ Sepal.Len ┆ Sepal.Wid ┆ Petal.Len ┆ Petal.Wid │
    #> │ th_sum     ┆ h_sum      ┆ th_sum     ┆ th_sum    ┆ gth_lette ┆ th_letter ┆ gth_lette ┆ th_letter │
    #> │ ---        ┆ ---        ┆ ---        ┆ ---       ┆ r         ┆ ---       ┆ r         ┆ ---       │
    #> │ f64        ┆ f64        ┆ f64        ┆ f64       ┆ ---       ┆ str       ┆ ---       ┆ str       │
    #> │            ┆            ┆            ┆           ┆ str       ┆           ┆ str       ┆           │
    #> ╞════════════╪════════════╪════════════╪═══════════╪═══════════╪═══════════╪═══════════╪═══════════╡
    #> │ 15.1       ┆ 13.5       ┆ 11.4       ┆ 10.2      ┆ f         ┆ d         ┆ b         ┆ a         │
    #> │ 14.9       ┆ 13.0       ┆ 11.4       ┆ 10.2      ┆ e         ┆ c         ┆ b         ┆ a         │
    #> │ 14.7       ┆ 13.2       ┆ 11.3       ┆ 10.2      ┆ e         ┆ d         ┆ b         ┆ a         │
    #> │ 14.6       ┆ 13.1       ┆ 11.5       ┆ 10.2      ┆ e         ┆ d         ┆ b         ┆ a         │
    #> │ 15.0       ┆ 13.6       ┆ 11.4       ┆ 10.2      ┆ e         ┆ d         ┆ b         ┆ a         │
    #> │ …          ┆ …          ┆ …          ┆ …         ┆ …         ┆ …         ┆ …         ┆ …         │
    #> │ 16.7       ┆ 13.0       ┆ 15.2       ┆ 12.3      ┆ g         ┆ c         ┆ f         ┆ c         │
    #> │ 16.3       ┆ 12.5       ┆ 15.0       ┆ 11.9      ┆ g         ┆ c         ┆ e         ┆ b         │
    #> │ 16.5       ┆ 13.0       ┆ 15.2       ┆ 12.0      ┆ g         ┆ c         ┆ f         ┆ b         │
    #> │ 16.2       ┆ 13.4       ┆ 15.4       ┆ 12.3      ┆ g         ┆ d         ┆ f         ┆ c         │
    #> │ 15.9       ┆ 13.0       ┆ 15.1       ┆ 11.8      ┆ f         ┆ c         ┆ f         ┆ b         │
    #> └────────────┴────────────┴────────────┴───────────┴───────────┴───────────┴───────────┴───────────┘

``` r
# Small benchmark --------------------------------

# Using `$map_elements()` is much slower than a more polars-native approach.
# First we multiply each element of a Series of 1M elements by 2.
n = 1000000L
set.seed(1)
df = pl$DataFrame(list(
  a = 1:n,
  b = sample(letters, n, replace = TRUE)
))

system.time({
  df$with_columns(
    bob = pl$col("a")$map_elements(\(x) {
      x * 2L
    })
  )
})
```

    #>    user  system elapsed 
    #>   2.355   0.005   2.499

``` r
# Comparing this to the standard polars syntax:
system.time({
  df$with_columns(
    bob = pl$col("a") * 2L
  )
})
```

    #>    user  system elapsed 
    #>   0.000   0.004   0.003

``` r
# Running in parallel --------------------------------

# here, we use Sys.sleep() to imitate some CPU expensive computation.

# use apply over each Species-group in each column equal to 12 sequential
# runs ~1.2 sec.
system.time({
  pl$LazyFrame(iris)$group_by("Species")$agg(
    pl$all()$map_elements(\(s) {
      Sys.sleep(.1)
      s$sum()
    })
  )$collect()
})
```

    #>    user  system elapsed 
    #>   0.031   0.001   1.234

``` r
# first run in parallel: there is some overhead to start up extra R processes
# drop any previous processes, just to show start-up overhead here
options(polars.rpool_cap = 0)
# set back to 4, the default
options(polars.rpool_cap = 4)
polars_options()$rpool_cap
```

    #> [1] 4

``` r
system.time({
  pl$LazyFrame(iris)$group_by("Species")$agg(
    pl$all()$map_elements(\(s) {
      Sys.sleep(.1)
      s$sum()
    }, in_background = TRUE)
  )$collect()
})
```

    #>    user  system elapsed 
    #>   0.013   0.004   1.151

``` r
# second run in parallel: this reuses R processes in "polars global_rpool".
polars_options()$rpool_cap
```

    #> [1] 4

``` r
system.time({
  pl$LazyFrame(iris)$group_by("Species")$agg(
    pl$all()$map_elements(\(s) {
      Sys.sleep(.1)
      s$sum()
    }, in_background = TRUE)
  )$collect()
})
```

    #>    user  system elapsed 
    #>   0.010   0.004   0.338
