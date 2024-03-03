

# Find local maxima

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__expr.R#L3284)

## Description

A local maximum is the point that marks the transition between an
increase and a decrease in a Series. The first and last values of the
Series can never be a peak.

## Usage

<pre><code class='language-R'>Expr_peak_max()
</code></pre>

## Value

Expr

## See Also

<code style="white-space: pre;">$peak_min()</code>

## Examples

``` r
library(polars)

df = pl$DataFrame(x = c(1, 2, 3, 2, 3, 4, 5, 2))
df
```

    #> shape: (8, 1)
    #> ┌─────┐
    #> │ x   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> │ 2.0 │
    #> │ 3.0 │
    #> │ 2.0 │
    #> │ 3.0 │
    #> │ 4.0 │
    #> │ 5.0 │
    #> │ 2.0 │
    #> └─────┘

``` r
df$with_columns(peak_max = pl$col("x")$peak_max())
```

    #> shape: (8, 2)
    #> ┌─────┬──────────┐
    #> │ x   ┆ peak_max │
    #> │ --- ┆ ---      │
    #> │ f64 ┆ bool     │
    #> ╞═════╪══════════╡
    #> │ 1.0 ┆ false    │
    #> │ 2.0 ┆ false    │
    #> │ 3.0 ┆ true     │
    #> │ 2.0 ┆ false    │
    #> │ 3.0 ┆ false    │
    #> │ 4.0 ┆ false    │
    #> │ 5.0 ┆ true     │
    #> │ 2.0 ┆ false    │
    #> └─────┴──────────┘
