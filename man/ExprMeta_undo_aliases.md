
# Undo aliases

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__meta.R#L122)

## Description

Undo any renaming operation like <code>alias</code> or
<code>keep_name</code>.

## Usage

<pre><code class='language-R'>ExprMeta_undo_aliases()
</code></pre>

## Value

Expr with aliases undone

## Examples

``` r
library(polars)

e = pl$col("alice")$alias("bob")
e$meta$root_names() == "alice"
```

    #> [1] TRUE

``` r
e$meta$output_name() == "bob"
```

    #> [1] TRUE

``` r
e$meta$undo_aliases()$meta$output_name() == "alice"
```

    #> [1] TRUE
