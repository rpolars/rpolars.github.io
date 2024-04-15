

# Convert an existing DataFrame to a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

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

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"
