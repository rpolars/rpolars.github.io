

# Get column by index

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/dataframe__frame.R#L610)

## Description

Extract a DataFrame column (by index) as a Polars series. Unlike
<code>get_column()</code>, this method will not fail but will return a
<code>NULL</code> if the index doesn’t exist in the DataFrame. Keep in
mind that Polars is 0-indexed so "0" is the first column.

## Usage

<pre><code class='language-R'>DataFrame_to_series(idx = 0)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_to_series_:_idx">idx</code>
</td>
<td>
Index of the column to return as Series. Defaults to 0, which is the
first column.
</td>
</tr>
</table>

## Value

Series or NULL

## Examples

``` r
library(polars)

df = pl$DataFrame(iris[1:10, ])

# default is to extract the first column
df$to_series()
```

    #> polars Series: shape: (10,)
    #> Series: 'Sepal.Length' [f64]
    #> [
    #>  5.1
    #>  4.9
    #>  4.7
    #>  4.6
    #>  5.0
    #>  5.4
    #>  4.6
    #>  5.0
    #>  4.4
    #>  4.9
    #> ]

``` r
# Polars is 0-indexed, so we use idx = 1 to extract the *2nd* column
df$to_series(idx = 1)
```

    #> polars Series: shape: (10,)
    #> Series: 'Sepal.Width' [f64]
    #> [
    #>  3.5
    #>  3.0
    #>  3.2
    #>  3.1
    #>  3.6
    #>  3.9
    #>  3.4
    #>  3.4
    #>  2.9
    #>  3.1
    #> ]

``` r
# doesn't error if the column isn't there
df$to_series(idx = 8)
```

    #> NULL
