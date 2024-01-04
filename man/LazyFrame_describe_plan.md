
# Print the optimized or non-optimized plans of <code>LazyFrame</code>

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/#L)

## Description

<code style="white-space: pre;">$describe_plan()</code> shows the query
in the format that <code>polars</code> understands.
<code style="white-space: pre;">$describe_optimized_plan()</code> shows
the optimized query plan that <code>polars</code> will execute when
<code style="white-space: pre;">$collect()</code> is called. It is
possible that both plans are identical if <code>polars</code> doesn’t
find any way to optimize the query.

## Usage

<pre><code class='language-R'>LazyFrame_describe_optimized_plan()

LazyFrame_describe_plan
</code></pre>

## Format

An object of class <code>character</code> of length 1.

## Value

This only prints the plan in the console, it doesn’t return any value.

## Examples

``` r
library(polars)

lazy_frame = pl$LazyFrame(iris)

# Prepare your query
lazy_query = lazy_frame$sort("Species")$filter(pl$col("Species") != "setosa")

# This is the query as `polars` understands it
lazy_query$describe_plan()
```

    #> FILTER [(col("Species")) != (String(setosa))] FROM
    #> SORT BY [col("Species")]
    #>   DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"

``` r
# This is the query after `polars` optimizes it: instead of sorting first and
# then filtering, it is faster to filter first and then sort the rest.
lazy_query$describe_optimized_plan()
```

    #> SORT BY [col("Species")]
    #>   DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "[(col(\"Species\")) != (String(setosa))]"
