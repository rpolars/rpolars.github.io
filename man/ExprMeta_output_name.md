

# Get the output column names

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/expr__meta.R#L98)

## Description

Get the column name that this expression would produce. It might not
always be possible to determine the output name as it might depend on
the schema of the context. In that case this will raise an error. Use
<code>$meta$root_names()</code> to get the name of input column.

## Usage

<pre><code class='language-R'>ExprMeta_output_name()
</code></pre>

## Value

A character vector

## Examples

``` r
library(polars)

e = (pl$col("alice") + pl$col("eve"))$alias("bob")
e$meta$output_name()
```

    #> [1] "bob"
