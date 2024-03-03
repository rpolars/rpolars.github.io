

# Undo any renaming operation

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__meta.R#L114)

## Description

This removes any renaming operation like <code>$alias()</code> or
<code>$name$keep()</code>. Polars uses the "leftmost rule" to determine
naming, meaning that the first element of the expression will be used to
name the output.

## Usage

<pre><code class='language-R'>ExprMeta_undo_aliases()
</code></pre>

## Value

Expr with aliases undone

## Examples

``` r
library(polars)

e = (pl$col("alice") + pl$col("eve"))$alias("bob")
e$meta$output_name()
```

    #> [1] "bob"

``` r
e$meta$undo_aliases()$meta$output_name()
```

    #> [1] "alice"
