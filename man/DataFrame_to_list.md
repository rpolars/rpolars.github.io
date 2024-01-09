
# Return Polars DataFrame as a list of vectors

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/dataframe__frame.R#L882)

## Description

Return Polars DataFrame as a list of vectors

## Usage

<pre><code class='language-R'>DataFrame_to_list(unnest_structs = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_to_list_:_unnest_structs">unnest_structs</code>
</td>
<td>
Boolean. If <code>TRUE</code> (default), then
<code style="white-space: pre;">$unnest()</code> is applied on any
struct column.
</td>
</tr>
</table>

## Details

For simplicity reasons, this implementation relies on unnesting all
structs before exporting to R. If <code>unnest_structs = FALSE</code>,
then <code>struct</code> columns will be returned as nested lists, where
each row is a list of values. Such a structure is not very typical or
efficient in R.

## Value

R list of vectors

## Examples

``` r
library(polars)

pl$DataFrame(iris)$to_list()
```

    #> $Sepal.Length
    #>   [1] 5.1 4.9 4.7 4.6 5.0 5.4 4.6 5.0 4.4 4.9 5.4 4.8 4.8 4.3 5.8 5.7 5.4 5.1
    #>  [19] 5.7 5.1 5.4 5.1 4.6 5.1 4.8 5.0 5.0 5.2 5.2 4.7 4.8 5.4 5.2 5.5 4.9 5.0
    #>  [37] 5.5 4.9 4.4 5.1 5.0 4.5 4.4 5.0 5.1 4.8 5.1 4.6 5.3 5.0 7.0 6.4 6.9 5.5
    #>  [55] 6.5 5.7 6.3 4.9 6.6 5.2 5.0 5.9 6.0 6.1 5.6 6.7 5.6 5.8 6.2 5.6 5.9 6.1
    #>  [73] 6.3 6.1 6.4 6.6 6.8 6.7 6.0 5.7 5.5 5.5 5.8 6.0 5.4 6.0 6.7 6.3 5.6 5.5
    #>  [91] 5.5 6.1 5.8 5.0 5.6 5.7 5.7 6.2 5.1 5.7 6.3 5.8 7.1 6.3 6.5 7.6 4.9 7.3
    #> [109] 6.7 7.2 6.5 6.4 6.8 5.7 5.8 6.4 6.5 7.7 7.7 6.0 6.9 5.6 7.7 6.3 6.7 7.2
    #> [127] 6.2 6.1 6.4 7.2 7.4 7.9 6.4 6.3 6.1 7.7 6.3 6.4 6.0 6.9 6.7 6.9 5.8 6.8
    #> [145] 6.7 6.7 6.3 6.5 6.2 5.9
    #> 
    #> $Sepal.Width
    #>   [1] 3.5 3.0 3.2 3.1 3.6 3.9 3.4 3.4 2.9 3.1 3.7 3.4 3.0 3.0 4.0 4.4 3.9 3.5
    #>  [19] 3.8 3.8 3.4 3.7 3.6 3.3 3.4 3.0 3.4 3.5 3.4 3.2 3.1 3.4 4.1 4.2 3.1 3.2
    #>  [37] 3.5 3.6 3.0 3.4 3.5 2.3 3.2 3.5 3.8 3.0 3.8 3.2 3.7 3.3 3.2 3.2 3.1 2.3
    #>  [55] 2.8 2.8 3.3 2.4 2.9 2.7 2.0 3.0 2.2 2.9 2.9 3.1 3.0 2.7 2.2 2.5 3.2 2.8
    #>  [73] 2.5 2.8 2.9 3.0 2.8 3.0 2.9 2.6 2.4 2.4 2.7 2.7 3.0 3.4 3.1 2.3 3.0 2.5
    #>  [91] 2.6 3.0 2.6 2.3 2.7 3.0 2.9 2.9 2.5 2.8 3.3 2.7 3.0 2.9 3.0 3.0 2.5 2.9
    #> [109] 2.5 3.6 3.2 2.7 3.0 2.5 2.8 3.2 3.0 3.8 2.6 2.2 3.2 2.8 2.8 2.7 3.3 3.2
    #> [127] 2.8 3.0 2.8 3.0 2.8 3.8 2.8 2.8 2.6 3.0 3.4 3.1 3.0 3.1 3.1 3.1 2.7 3.2
    #> [145] 3.3 3.0 2.5 3.0 3.4 3.0
    #> 
    #> $Petal.Length
    #>   [1] 1.4 1.4 1.3 1.5 1.4 1.7 1.4 1.5 1.4 1.5 1.5 1.6 1.4 1.1 1.2 1.5 1.3 1.4
    #>  [19] 1.7 1.5 1.7 1.5 1.0 1.7 1.9 1.6 1.6 1.5 1.4 1.6 1.6 1.5 1.5 1.4 1.5 1.2
    #>  [37] 1.3 1.4 1.3 1.5 1.3 1.3 1.3 1.6 1.9 1.4 1.6 1.4 1.5 1.4 4.7 4.5 4.9 4.0
    #>  [55] 4.6 4.5 4.7 3.3 4.6 3.9 3.5 4.2 4.0 4.7 3.6 4.4 4.5 4.1 4.5 3.9 4.8 4.0
    #>  [73] 4.9 4.7 4.3 4.4 4.8 5.0 4.5 3.5 3.8 3.7 3.9 5.1 4.5 4.5 4.7 4.4 4.1 4.0
    #>  [91] 4.4 4.6 4.0 3.3 4.2 4.2 4.2 4.3 3.0 4.1 6.0 5.1 5.9 5.6 5.8 6.6 4.5 6.3
    #> [109] 5.8 6.1 5.1 5.3 5.5 5.0 5.1 5.3 5.5 6.7 6.9 5.0 5.7 4.9 6.7 4.9 5.7 6.0
    #> [127] 4.8 4.9 5.6 5.8 6.1 6.4 5.6 5.1 5.6 6.1 5.6 5.5 4.8 5.4 5.6 5.1 5.1 5.9
    #> [145] 5.7 5.2 5.0 5.2 5.4 5.1
    #> 
    #> $Petal.Width
    #>   [1] 0.2 0.2 0.2 0.2 0.2 0.4 0.3 0.2 0.2 0.1 0.2 0.2 0.1 0.1 0.2 0.4 0.4 0.3
    #>  [19] 0.3 0.3 0.2 0.4 0.2 0.5 0.2 0.2 0.4 0.2 0.2 0.2 0.2 0.4 0.1 0.2 0.2 0.2
    #>  [37] 0.2 0.1 0.2 0.2 0.3 0.3 0.2 0.6 0.4 0.3 0.2 0.2 0.2 0.2 1.4 1.5 1.5 1.3
    #>  [55] 1.5 1.3 1.6 1.0 1.3 1.4 1.0 1.5 1.0 1.4 1.3 1.4 1.5 1.0 1.5 1.1 1.8 1.3
    #>  [73] 1.5 1.2 1.3 1.4 1.4 1.7 1.5 1.0 1.1 1.0 1.2 1.6 1.5 1.6 1.5 1.3 1.3 1.3
    #>  [91] 1.2 1.4 1.2 1.0 1.3 1.2 1.3 1.3 1.1 1.3 2.5 1.9 2.1 1.8 2.2 2.1 1.7 1.8
    #> [109] 1.8 2.5 2.0 1.9 2.1 2.0 2.4 2.3 1.8 2.2 2.3 1.5 2.3 2.0 2.0 1.8 2.1 1.8
    #> [127] 1.8 1.8 2.1 1.6 1.9 2.0 2.2 1.5 1.4 2.3 2.4 1.8 1.8 2.1 2.4 2.3 1.9 2.3
    #> [145] 2.5 2.3 1.9 2.0 2.3 1.8
    #> 
    #> $Species
    #>   [1] setosa     setosa     setosa     setosa     setosa     setosa    
    #>   [7] setosa     setosa     setosa     setosa     setosa     setosa    
    #>  [13] setosa     setosa     setosa     setosa     setosa     setosa    
    #>  [19] setosa     setosa     setosa     setosa     setosa     setosa    
    #>  [25] setosa     setosa     setosa     setosa     setosa     setosa    
    #>  [31] setosa     setosa     setosa     setosa     setosa     setosa    
    #>  [37] setosa     setosa     setosa     setosa     setosa     setosa    
    #>  [43] setosa     setosa     setosa     setosa     setosa     setosa    
    #>  [49] setosa     setosa     versicolor versicolor versicolor versicolor
    #>  [55] versicolor versicolor versicolor versicolor versicolor versicolor
    #>  [61] versicolor versicolor versicolor versicolor versicolor versicolor
    #>  [67] versicolor versicolor versicolor versicolor versicolor versicolor
    #>  [73] versicolor versicolor versicolor versicolor versicolor versicolor
    #>  [79] versicolor versicolor versicolor versicolor versicolor versicolor
    #>  [85] versicolor versicolor versicolor versicolor versicolor versicolor
    #>  [91] versicolor versicolor versicolor versicolor versicolor versicolor
    #>  [97] versicolor versicolor versicolor versicolor virginica  virginica 
    #> [103] virginica  virginica  virginica  virginica  virginica  virginica 
    #> [109] virginica  virginica  virginica  virginica  virginica  virginica 
    #> [115] virginica  virginica  virginica  virginica  virginica  virginica 
    #> [121] virginica  virginica  virginica  virginica  virginica  virginica 
    #> [127] virginica  virginica  virginica  virginica  virginica  virginica 
    #> [133] virginica  virginica  virginica  virginica  virginica  virginica 
    #> [139] virginica  virginica  virginica  virginica  virginica  virginica 
    #> [145] virginica  virginica  virginica  virginica  virginica  virginica 
    #> Levels: setosa versicolor virginica
