
# Undo aliases

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__meta.R#L122)

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
