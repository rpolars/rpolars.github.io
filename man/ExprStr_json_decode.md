

# Parse string values as JSON.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L507)

## Description

Parse string values as JSON.

## Usage

<pre><code class='language-R'>ExprStr_json_decode(dtype, infer_schema_length = 100)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_json_decode_:_dtype">dtype</code>
</td>
<td>
The dtype to cast the extracted value to. If <code>NULL</code>, the
dtype will be inferred from the JSON value.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_json_decode_:_infer_schema_length">infer_schema_length</code>
</td>
<td>
How many rows to parse to determine the schema. If <code>NULL</code>,
all rows are used.
</td>
</tr>
</table>

## Details

Throw errors if encounter invalid json strings.

## Value

Expr returning a struct

## Examples

``` r
library(polars)

df = pl$DataFrame(
  json_val = c('{"a":1, "b": true}', NA, '{"a":2, "b": false}')
)
dtype = pl$Struct(pl$Field("a", pl$Int64), pl$Field("b", pl$Boolean))
df$select(pl$col("json_val")$str$json_decode(dtype))
```

    #> shape: (3, 1)
    #> ┌─────────────┐
    #> │ json_val    │
    #> │ ---         │
    #> │ struct[2]   │
    #> ╞═════════════╡
    #> │ {1,true}    │
    #> │ {null,null} │
    #> │ {2,false}   │
    #> └─────────────┘
