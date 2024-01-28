

# Convert an existing DataFrame to a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L20)

## Description

Start a new lazy query from a DataFrame.

## Usage

<pre><code class='language-R'>DataFrame_lazy()
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
