

# Drop in place

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/dataframe__frame.R#L680)

## Description

Drop a single column in-place and return the dropped column.

## Usage

<pre><code class='language-R'>DataFrame_drop_in_place(name)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_drop_in_place_:_name">name</code>
</td>
<td>
string Name of the column to drop.
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

dat = pl$DataFrame(iris)
x = dat$drop_in_place("Species")
x
```

    #> polars Series: shape: (150,)
    #> Series: 'Species' [cat]
    #> [
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  "setosa"
    #>  …
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #>  "virginica"
    #> ]

``` r
dat$columns
```

    #> [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width"
