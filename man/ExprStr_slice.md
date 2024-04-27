

# Create subslices of the string values of a String Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__string.R#L851)

## Description

Create subslices of the string values of a String Series

## Usage

<pre><code class='language-R'>ExprStr_slice(offset, length = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="offset">offset</code>
</td>
<td>
Start index. Negative indexing is supported.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="length">length</code>
</td>
<td>
Length of the slice. If <code>NULL</code> (default), the slice is taken
to the end of the string.
</td>
</tr>
</table>

## Value

Expr: Series of dtype String.

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
