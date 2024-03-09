

# Get the root column names

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/expr__meta.R#L83)

## Description

This returns the names of input columns. Use
<code>$meta$output_name()</code> to get the name of output column.

## Usage

<pre><code class='language-R'>ExprMeta_root_names()
</code></pre>

## Value

A character vector

## Examples

``` r
library(polars)

e = (pl$col("alice") + pl$col("eve"))$alias("bob")
e$meta$root_names()
```

    #> [1] "alice" "eve"
