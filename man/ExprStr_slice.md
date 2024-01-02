
# Create subslices of the string values of a Utf8 Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__string.R#L788)

## Description

Create subslices of the string values of a Utf8 Series

## Usage

<pre><code class='language-R'>ExprStr_slice(offset, length = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_slice_:_offset">offset</code>
</td>
<td>
Start index. Negative indexing is supported.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_slice_:_length">length</code>
</td>
<td>
Length of the slice. If <code>NULL</code> (default), the slice is taken
to the end of the string.
</td>
</tr>
</table>

## Value

Expr: Series of dtype Utf8.

## Examples

``` r
library(polars)

df = pl$DataFrame(s = c("pear", NA, "papaya", "dragonfruit"))
df$with_columns(
  pl$col("s")$str$slice(-3)$alias("s_sliced")
)
```

    #> shape: (4, 2)
    #> ┌─────────────┬──────────┐
    #> │ s           ┆ s_sliced │
    #> │ ---         ┆ ---      │
    #> │ str         ┆ str      │
    #> ╞═════════════╪══════════╡
    #> │ pear        ┆ ear      │
    #> │ null        ┆ null     │
    #> │ papaya      ┆ aya      │
    #> │ dragonfruit ┆ uit      │
    #> └─────────────┴──────────┘
