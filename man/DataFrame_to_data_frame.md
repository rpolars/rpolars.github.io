
# Return Polars DataFrame as R data.frame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L854)

## Description

Return Polars DataFrame as R data.frame

## Usage

<pre><code class='language-R'>DataFrame_to_data_frame(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_to_data_frame_:_...">…</code>
</td>
<td>
Any args pased to <code>as.data.frame()</code>.
</td>
</tr>
</table>

## Value

An R data.frame

## Examples

``` r
library(polars)

df = pl$DataFrame(iris[1:3, ])
df$to_data_frame()
```

    #>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    #> 1          5.1         3.5          1.4         0.2  setosa
    #> 2          4.9         3.0          1.4         0.2  setosa
    #> 3          4.7         3.2          1.3         0.2  setosa
