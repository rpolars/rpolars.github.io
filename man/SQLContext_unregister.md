

# Unregister tables by name

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/sql.R#L140)

## Description

Unregister tables by name.

## Usage

<pre><code class='language-R'>SQLContext_unregister(names)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="SQLContext_unregister_:_names">names</code>
</td>
<td>
A character vector of table names to unregister.
</td>
</tr>
</table>

## Value

Returns the SQLContext_class object invisibly.

## Examples

``` r
library(polars)


# Initialise a new SQLContext and register the given tables.
ctx = pl$SQLContext(x = mtcars, y = mtcars, z = mtcars)
ctx$tables()
```

    #> [1] "x" "y" "z"

``` r
# Unregister some tables.
ctx$unregister(c("x", "y"))
ctx$tables()
```

    #> [1] "z"
