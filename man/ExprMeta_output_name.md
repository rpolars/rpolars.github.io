

# Get the column name that this expression would produce

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__meta.R#L115)

## Description

It may not always be possible to determine the output name as that can
depend on the schema of the context; in that case this will raise an
error if <code>raise_if_undetermined</code> is <code>TRUE</code> (the
default), or return <code>NA</code> otherwise.

## Usage

<pre><code class='language-R'>ExprMeta_output_name(..., raise_if_undetermined = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprMeta_output_name_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprMeta_output_name_:_raise_if_undetermined">raise_if_undetermined</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if the output name cannot
be determined. Otherwise, return <code>NA</code>.
</td>
</tr>
</table>

## Value

A character vector

## Examples

``` r
library(polars)

e = pl$col("foo") * pl$col("bar")
e$meta$output_name()
```

    #> [1] "foo"

``` r
e_filter = pl$col("foo")$filter(pl$col("bar") == 13)
e_filter$meta$output_name()
```

    #> [1] "foo"

``` r
e_sum_over = pl$sum("foo")$over("groups")
e_sum_over$meta$output_name()
```

    #> [1] "foo"

``` r
e_sum_slice = pl$sum("foo")$slice(pl$len() - 10, pl$col("bar"))
e_sum_slice$meta$output_name()
```

    #> [1] "foo"

``` r
pl$len()$meta$output_name()
```

    #> [1] "len"

``` r
pl$col("*")$meta$output_name(raise_if_undetermined = FALSE)
```

    #> [1] NA
