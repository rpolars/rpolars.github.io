
# Output Name

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__meta.R#L107)

## Description

Get the column name that this expression would produce. It might not
always be possible to determine the output name as it might depend on
the schema of the context. In that case this will raise an error.

## Usage

<pre><code class='language-R'>ExprMeta_output_name()
</code></pre>

## Value

R charvec of output names.

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
