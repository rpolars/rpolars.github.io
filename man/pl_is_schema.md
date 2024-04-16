

# check if schema

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/datatype.R#L8)

## Description

check if schema

## Usage

<pre><code class='language-R'>pl_is_schema(x)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_is_schema_:_x">x</code>
</td>
<td>
object to test if schema
</td>
</tr>
</table>

## Value

bool

## Examples

``` r
library(polars)

pl$is_schema(pl$DataFrame(iris)$schema)
```

    #> [1] TRUE

``` r
pl$is_schema(list("alice", "bob"))
```

    #> [1] FALSE
