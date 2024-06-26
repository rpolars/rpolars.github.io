

# Glimpse values in a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1753)

## Description

Glimpse values in a DataFrame

## Usage

<pre><code class='language-R'>DataFrame_glimpse(..., return_as_string = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
not used
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="return_as_string">return_as_string</code>
</td>
<td>
Logical (default <code>FALSE</code>). If <code>TRUE</code>, return the
output as a string.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(iris)$glimpse()
```

    #> & Sepal.Length <f64> 5.1, 4.9, 4.7, 4.6, 5, 5.4, 4.6, 5, 4.4, 4.9
    #> & Sepal.Width  <f64> 3.5, 3, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1
    #> & Petal.Length <f64> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5
    #> & Petal.Width  <f64> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1
    #> & Species      <cat> setosa, setosa, setosa, setosa, setosa, setosa, setosa, setosa, setosa, setosa
