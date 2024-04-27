

# Convert an existing DataFrame to a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

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
