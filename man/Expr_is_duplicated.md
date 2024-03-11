

# Check whether each value is duplicated

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/after-wrappers.R#L20)

## Description

This is syntactic sugar for
<code style="white-space: pre;">$is_unique()$not()</code>.

## Usage

<pre><code class='language-R'>Expr_is_duplicated()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(head(mtcars[, 1:2]))$
  with_columns(is_duplicated = pl$col("mpg")$is_duplicated())
```

    #> shape: (6, 3)
    #> ┌──────┬─────┬───────────────┐
    #> │ mpg  ┆ cyl ┆ is_duplicated │
    #> │ ---  ┆ --- ┆ ---           │
    #> │ f64  ┆ f64 ┆ bool          │
    #> ╞══════╪═════╪═══════════════╡
    #> │ 21.0 ┆ 6.0 ┆ true          │
    #> │ 21.0 ┆ 6.0 ┆ true          │
    #> │ 22.8 ┆ 4.0 ┆ false         │
    #> │ 21.4 ┆ 6.0 ┆ false         │
    #> │ 18.7 ┆ 8.0 ┆ false         │
    #> │ 18.1 ┆ 6.0 ┆ false         │
    #> └──────┴─────┴───────────────┘
