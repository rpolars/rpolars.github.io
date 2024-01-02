
# Data types information

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/lazyframe__lazy.R#L1300)

## Description

Get the data type of all columns. You can see all available types with
<code>names(pl$dtypes)</code>. The data type of each column is also
shown when printing the DataFrame.

## Usage

<pre><code class='language-R'>LazyFrame_schema()

LazyFrame_dtypes()
</code></pre>

## Value

<code style="white-space: pre;">$dtypes</code> returns an unnamed list
with the data type of each column.
<code style="white-space: pre;">$schema</code> returns a named list with
the column names and the data type of each column.

## Examples

``` r
library(polars)

pl$LazyFrame(iris)$dtypes
```

    #> [[1]]
    #> DataType: Float64
    #> 
    #> [[2]]
    #> DataType: Float64
    #> 
    #> [[3]]
    #> DataType: Float64
    #> 
    #> [[4]]
    #> DataType: Float64
    #> 
    #> [[5]]
    #> DataType: Categorical(
    #>     Some(
    #>         local,
    #>     ),
    #>     Physical,
    #> )

``` r
pl$LazyFrame(iris)$schema
```

    #> $Sepal.Length
    #> DataType: Float64
    #> 
    #> $Sepal.Width
    #> DataType: Float64
    #> 
    #> $Petal.Length
    #> DataType: Float64
    #> 
    #> $Petal.Width
    #> DataType: Float64
    #> 
    #> $Species
    #> DataType: Categorical(
    #>     Some(
    #>         local,
    #>     ),
    #>     Physical,
    #> )
