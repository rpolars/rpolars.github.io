
# Convert an existing DataFrame to a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Start a new lazy query from a DataFrame.

## Usage

<pre><code class='language-R'>DataFrame_lazy
</code></pre>

## Value

A LazyFrame

## Examples

``` r
library(polars)

pl$DataFrame(iris)$lazy()
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"
