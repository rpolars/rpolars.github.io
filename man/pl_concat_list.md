

# Concat the arrays in a Series dtype List in linear time.

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/functions__lazy.R#L591)

## Description

Folds the expressions from left to right, keeping the first non-null
value.

## Usage

<pre><code class='language-R'>pl_concat_list(exprs)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="exprs">exprs</code>
</td>
<td>
list of Into<Expr>, strings interpreted as column names
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

# Create lagged columns and collect them into a list. This mimics a rolling window.
df = pl$DataFrame(A = c(1, 2, 9, 2, 13))
df$with_columns(lapply(
  0:2,
  \(i) pl$col("A")$shift(i)$alias(paste0("A_lag_", i))
))$select(
  pl$concat_list(lapply(2:0, \(i) pl$col(paste0("A_lag_", i))))$alias(
    "A_rolling"
  )
)
```

    #> shape: (5, 1)
    #> ┌───────────────────┐
    #> │ A_rolling         │
    #> │ ---               │
    #> │ list[f64]         │
    #> ╞═══════════════════╡
    #> │ [null, null, 1.0] │
    #> │ [null, 1.0, 2.0]  │
    #> │ [1.0, 2.0, 9.0]   │
    #> │ [2.0, 9.0, 2.0]   │
    #> │ [9.0, 2.0, 13.0]  │
    #> └───────────────────┘

``` r
# concat Expr a Series and an R obejct
pl$concat_list(list(
  pl$lit(1:5),
  as_polars_series(5:1),
  rep(0L, 5)
))$alias("alice")$to_series()
```

    #> polars Series: shape: (5,)
    #> Series: 'alice' [list[i32]]
    #> [
    #>  [1, 5, 0]
    #>  [2, 4, 0]
    #>  [3, 3, 0]
    #>  [4, 2, 0]
    #>  [5, 1, 0]
    #> ]
