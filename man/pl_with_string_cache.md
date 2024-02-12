

# Evaluate one or several expressions with global string cache

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/polars_options.R#L320)

## Description

This function only temporarily enables the global string cache.

## Usage

<pre><code class='language-R'>pl_with_string_cache(expr)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_with_string_cache_:_expr">expr</code>
</td>
<td>
An Expr to evaluate while the string cache is enabled.
</td>
</tr>
</table>

## Value

return value of expression

## See Also

<code>pl$using_string_cache</code> <code>pl$enable_enable_cache</code>

## Examples

``` r
library(polars)

# activate string cache temporarily when constructing two DataFrame's
pl$with_string_cache({
  df1 = pl$DataFrame(head(iris, 2))
  df2 = pl$DataFrame(tail(iris, 2))
})
```

    #> shape: (2, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat       │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╡
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┘

``` r
pl$concat(list(df1, df2))
```

    #> shape: (4, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat       │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┘
