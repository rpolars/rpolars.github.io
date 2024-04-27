

# Initialise a new SQLContext

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/sql.R#L39)

## Description

Create a new SQLContext and register the given LazyFrames.

## Usage

<pre><code class='language-R'>pl_SQLContext(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Name-value pairs of LazyFrame like objects to register.
</td>
</tr>
</table>

## Value

An SQLContext

## Examples

``` r
library(polars)


ctx = pl$SQLContext(mtcars = mtcars)
ctx
```

    #> RPolarsSQLContext
    #>   tables: mtcars
