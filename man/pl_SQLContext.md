

# Initialise a new SQLContext

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/sql.R#L39)

## Description

Create a new SQLContext and register the given LazyFrames.

## Usage

<pre><code class='language-R'>pl_SQLContext(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_SQLContext_:_...">…</code>
</td>
<td>
Name-value pairs of LazyFrame like objects to register.
</td>
</tr>
</table>

## Value

RPolarsSQLContext

## Examples

``` r
library(polars)


ctx = pl$SQLContext(mtcars = mtcars)
ctx
```

    #> RPolarsSQLContext
    #>   tables: mtcars
