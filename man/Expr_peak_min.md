

# Find local minima

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3408)

## Description

A local minimum is the point that marks the transition between a
decrease and an increase in a Series. The first and last values of the
Series can never be a peak.

## Usage

<pre><code class='language-R'>Expr_peak_min()
</code></pre>

## Value

Expr

## See Also

<code style="white-space: pre;">$peak_max()</code>

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
df$with_columns(peak_min = pl$col("x")$peak_min())
```

    #> shape: (8, 2)
    #> ┌─────┬──────────┐
    #> │ x   ┆ peak_min │
    #> │ --- ┆ ---      │
    #> │ f64 ┆ bool     │
    #> ╞═════╪══════════╡
    #> │ 1.0 ┆ false    │
    #> │ 2.0 ┆ false    │
    #> │ 3.0 ┆ false    │
    #> │ 2.0 ┆ true     │
    #> │ 3.0 ┆ false    │
    #> │ 4.0 ┆ false    │
    #> │ 5.0 ┆ false    │
    #> │ 2.0 ┆ false    │
    #> └─────┴──────────┘
