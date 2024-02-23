

# Check if an expression is between the given lower and upper bounds

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2233)

## Description

Check if an expression is between the given lower and upper bounds

## Usage

<pre><code class='language-R'>Expr_is_between(lower_bound, upper_bound, closed = "both")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_is_between_:_lower_bound">lower_bound</code>
</td>
<td>
Lower bound, can be an Expr. Strings are parsed as column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_is_between_:_upper_bound">upper_bound</code>
</td>
<td>
Upper bound, can be an Expr. Strings are parsed as column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_is_between_:_closed">closed</code>
</td>
<td>
Define which sides of the interval are closed (inclusive). This can be
either <code>“left”</code>, <code>“right”</code>, <code>“both”</code> or
<code>“none”</code>.
</td>
</tr>
</table>

## Details

Note that in polars, <code>NaN</code> are equal to other
<code>NaN</code>s, and greater than any non-<code>NaN</code> value.

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(num = 1:5)
df$with_columns(
  is_between = pl$col("num")$is_between(2, 4),
  is_between_excl_upper = pl$col("num")$is_between(2, 4, closed = "left"),
  is_between_excl_both = pl$col("num")$is_between(2, 4, closed = "none")
)
```

    #> shape: (5, 4)
    #> ┌─────┬────────────┬───────────────────────┬──────────────────────┐
    #> │ num ┆ is_between ┆ is_between_excl_upper ┆ is_between_excl_both │
    #> │ --- ┆ ---        ┆ ---                   ┆ ---                  │
    #> │ i32 ┆ bool       ┆ bool                  ┆ bool                 │
    #> ╞═════╪════════════╪═══════════════════════╪══════════════════════╡
    #> │ 1   ┆ false      ┆ false                 ┆ false                │
    #> │ 2   ┆ true       ┆ true                  ┆ false                │
    #> │ 3   ┆ true       ┆ true                  ┆ true                 │
    #> │ 4   ┆ true       ┆ false                 ┆ false                │
    #> │ 5   ┆ false      ┆ false                 ┆ false                │
    #> └─────┴────────────┴───────────────────────┴──────────────────────┘

``` r
# lower and upper bounds can also be column names or expr
df = pl$DataFrame(
  num = 1:5,
  lower = c(0, 2, 3, 3, 3),
  upper = c(6, 4, 4, 8, 3.5)
)
df$with_columns(
  is_between_cols = pl$col("num")$is_between("lower", "upper"),
  is_between_expr = pl$col("num")$is_between(pl$col("lower") / 2, "upper")
)
```

    #> shape: (5, 5)
    #> ┌─────┬───────┬───────┬─────────────────┬─────────────────┐
    #> │ num ┆ lower ┆ upper ┆ is_between_cols ┆ is_between_expr │
    #> │ --- ┆ ---   ┆ ---   ┆ ---             ┆ ---             │
    #> │ i32 ┆ f64   ┆ f64   ┆ bool            ┆ bool            │
    #> ╞═════╪═══════╪═══════╪═════════════════╪═════════════════╡
    #> │ 1   ┆ 0.0   ┆ 6.0   ┆ true            ┆ true            │
    #> │ 2   ┆ 2.0   ┆ 4.0   ┆ true            ┆ true            │
    #> │ 3   ┆ 3.0   ┆ 4.0   ┆ true            ┆ true            │
    #> │ 4   ┆ 3.0   ┆ 8.0   ┆ true            ┆ true            │
    #> │ 5   ┆ 3.0   ┆ 3.5   ┆ false           ┆ false           │
    #> └─────┴───────┴───────┴─────────────────┴─────────────────┘
