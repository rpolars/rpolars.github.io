

# Compare two DataFrames

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/dataframe__frame.R#L739)

## Description

Check if two DataFrames are equal.

## Usage

<pre><code class='language-R'>DataFrame_equals(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_equals_:_other">other</code>
</td>
<td>
DataFrame to compare with.
</td>
</tr>
</table>

## Value

A boolean.

## Examples

``` r
library(polars)

dat1 = pl$DataFrame(iris)
dat2 = pl$DataFrame(iris)
dat3 = pl$DataFrame(mtcars)
dat1$equals(dat2)
```

    #> [1] TRUE

``` r
dat1$equals(dat3)
```

    #> [1] FALSE
