
# Get columns (as Series)

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Extract all DataFrame columns as a list of Polars series.

## Usage

<pre><code class='language-R'>DataFrame_get_columns()
</code></pre>

## Value

A list of series

## Examples

``` r
library(polars)

df = pl$DataFrame(iris[1:2, ])
df$get_columns()
```

    #> $Sepal.Length
    #> polars Series: shape: (2,)
    #> Series: 'Sepal.Length' [f64]
    #> [
    #>  5.1
    #>  4.9
    #> ]
    #> 
    #> $Sepal.Width
    #> polars Series: shape: (2,)
    #> Series: 'Sepal.Width' [f64]
    #> [
    #>  3.5
    #>  3.0
    #> ]
    #> 
    #> $Petal.Length
    #> polars Series: shape: (2,)
    #> Series: 'Petal.Length' [f64]
    #> [
    #>  1.4
    #>  1.4
    #> ]
    #> 
    #> $Petal.Width
    #> polars Series: shape: (2,)
    #> Series: 'Petal.Width' [f64]
    #> [
    #>  0.2
    #>  0.2
    #> ]
    #> 
    #> $Species
    #> polars Series: shape: (2,)
    #> Series: 'Species' [cat]
    #> [
    #>  "setosa"
    #>  "setosa"
    #> ]
