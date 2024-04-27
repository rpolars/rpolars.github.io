

# Get column (as one Series)

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/dataframe__frame.R#L638)

## Description

Extract a DataFrame column as a Polars series.

## Usage

<pre><code class='language-R'>DataFrame_get_column(name)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="name">name</code>
</td>
<td>
Name of the column to extract.
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

df = pl$DataFrame(iris[1:2, ])
df$get_column("Species")
```

    #> polars Series: shape: (2,)
    #> Series: 'Species' [cat]
    #> [
    #>  "setosa"
    #>  "setosa"
    #> ]
