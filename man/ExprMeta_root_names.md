

# Root Name

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__meta.R#L89)

## Description

Get a vector with the root column name

## Usage

<pre><code class='language-R'>ExprMeta_root_names()
</code></pre>

## Value

R charvec of root names.

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
