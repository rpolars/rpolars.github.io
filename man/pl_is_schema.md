
# check if schema

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/datatype.R#L9)

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

## Format

function

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
