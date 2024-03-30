

# Check whether a value is in a vector

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2071)

## Description

Notice that to check whether a factor value is in a vector of strings,
you need to use the string cache, either with
<code>pl$enable_string_cache()</code> or with
<code>pl$with_string_cache()</code>. See examples.

## Usage

<pre><code class='language-R'>Expr_is_in(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_is_in_:_other">other</code>
</td>
<td>
numeric or string value; accepts expression input.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(1:4, NA_integer_))$with_columns(
  in_1_3 = pl$col("a")$is_in(c(1, 3)),
  in_NA = pl$col("a")$is_in(pl$lit(NA_real_))
)
```

    #> shape: (5, 3)
    #> ┌──────┬────────┬───────┐
    #> │ a    ┆ in_1_3 ┆ in_NA │
    #> │ ---  ┆ ---    ┆ ---   │
    #> │ i32  ┆ bool   ┆ bool  │
    #> ╞══════╪════════╪═══════╡
    #> │ 1    ┆ true   ┆ false │
    #> │ 2    ┆ false  ┆ false │
    #> │ 3    ┆ true   ┆ false │
    #> │ 4    ┆ false  ┆ false │
    #> │ null ┆ null   ┆ null  │
    #> └──────┴────────┴───────┘

``` r
# this fails because we can't compare factors to strings
# pl$DataFrame(a = factor(letters[1:5]))$with_columns(
#   in_abc = pl$col("a")$is_in(c("a", "b", "c"))
# )

# need to use the string cache for this
pl$with_string_cache({
  pl$DataFrame(a = factor(letters[1:5]))$with_columns(
    in_abc = pl$col("a")$is_in(c("a", "b", "c"))
  )
})
```

    #> shape: (5, 2)
    #> ┌─────┬────────┐
    #> │ a   ┆ in_abc │
    #> │ --- ┆ ---    │
    #> │ cat ┆ bool   │
    #> ╞═════╪════════╡
    #> │ a   ┆ true   │
    #> │ b   ┆ true   │
    #> │ c   ┆ true   │
    #> │ d   ┆ false  │
    #> │ e   ┆ false  │
    #> └─────┴────────┘
