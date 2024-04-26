

# Extract the first match of JSON string with the provided JSONPath expression

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L550)

## Description

Extract the first match of JSON string with the provided JSONPath
expression

## Usage

<pre><code class='language-R'>ExprStr_json_path_match(json_path)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="json_path">json_path</code>
</td>
<td>
A valid JSON path query string.
</td>
</tr>
</table>

## Details

Throw errors if encounter invalid JSON strings. All return value will be
cast to String regardless of the original value.

Documentation on JSONPath standard can be found here:
<a href="https://goessner.net/articles/JsonPath/">https://goessner.net/articles/JsonPath/</a>.

## Value

String array. Contain null if original value is null or the json_path
return nothing.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  json_val = c('{"a":"1"}', NA, '{"a":2}', '{"a":2.1}', '{"a":true}')
)
df$select(pl$col("json_val")$str$json_path_match("$.a"))
```

    #> shape: (5, 1)
    #> ┌──────────┐
    #> │ json_val │
    #> │ ---      │
    #> │ str      │
    #> ╞══════════╡
    #> │ 1        │
    #> │ null     │
    #> │ 2        │
    #> │ 2.1      │
    #> │ true     │
    #> └──────────┘
