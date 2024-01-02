
# Check whether a value is between two values

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__expr.R#L2202)

## Description

This is syntactic sugar for <code>x \> start & x \< end</code> (or
<code>x \>= start & x \<= end</code>).

## Usage

<pre><code class='language-R'>Expr_is_between(start, end, include_bounds = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_is_between_:_start">start</code>
</td>
<td>
Lower bound, an Expr that is either numeric or datetime.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_is_between_:_end">end</code>
</td>
<td>
Upper bound, an Expr that is either numeric or datetime.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_is_between_:_include_bounds">include_bounds</code>
</td>
<td>
If <code>FALSE</code> (default), exclude start and end. This can also be
a vector of two booleans indicating whether to include the start and/or
the end.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(num = 1:5, y = c(0, 2, 3, 3, 3))
df$with_columns(
  bet_2_4_no_bounds = pl$col("num")$is_between(2, 4),
  bet_2_4_with_bounds = pl$col("num")$is_between(2, 4, TRUE),
  bet_2_4_upper_bound = pl$col("num")$is_between(2, 4, c(FALSE, TRUE)),
  between_y_4 = pl$col("num")$is_between(pl$col("y"), 6)
)
```

    #> shape: (5, 6)
    #> ┌─────┬─────┬───────────────────┬─────────────────────┬─────────────────────┬─────────────┐
    #> │ num ┆ y   ┆ bet_2_4_no_bounds ┆ bet_2_4_with_bounds ┆ bet_2_4_upper_bound ┆ between_y_4 │
    #> │ --- ┆ --- ┆ ---               ┆ ---                 ┆ ---                 ┆ ---         │
    #> │ i32 ┆ f64 ┆ bool              ┆ bool                ┆ bool                ┆ bool        │
    #> ╞═════╪═════╪═══════════════════╪═════════════════════╪═════════════════════╪═════════════╡
    #> │ 1   ┆ 0.0 ┆ false             ┆ false               ┆ false               ┆ true        │
    #> │ 2   ┆ 2.0 ┆ false             ┆ true                ┆ false               ┆ false       │
    #> │ 3   ┆ 3.0 ┆ true              ┆ true                ┆ true                ┆ false       │
    #> │ 4   ┆ 3.0 ┆ false             ┆ true                ┆ true                ┆ true        │
    #> │ 5   ┆ 3.0 ┆ false             ┆ false               ┆ false               ┆ true        │
    #> └─────┴─────┴───────────────────┴─────────────────────┴─────────────────────┴─────────────┘
