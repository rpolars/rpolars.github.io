

# Replace values by different values

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__expr.R#L3592)

## Description

This allows one to recode values in a column.

## Usage

<pre><code class='language-R'>Expr_replace(old, new, default = NULL, return_dtype = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_replace_:_old">old</code>
</td>
<td>

Can be several things:

<ul>
<li>

a vector indicating the values to recode;

</li>
<li>

if <code>new</code> is missing, this can be a named list e.g
<code>list(old = “new”)</code> where the names are the old values and
the values are the replacements. Note that if old values are numeric,
the names must be wrapped in backticks;

</li>
<li>

an Expr

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_replace_:_new">new</code>
</td>
<td>
Either a scalar, a vector of same length as <code>old</code> or an Expr.
If missing, <code>old</code> must be a named list.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_replace_:_default">default</code>
</td>
<td>
The default replacement if the value is not in <code>old</code>. Can be
an Expr. If <code>NULL</code> (default), then the value doesn’t change.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_replace_:_return_dtype">return_dtype</code>
</td>
<td>
The data type of the resulting expression. If set to <code>NULL</code>
(default), the data type is determined automatically based on the other
inputs.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c(1, 2, 2, 3))

# "old" and "new" can take either scalars or vectors of same length
df$with_columns(replaced = pl$col("a")$replace(2, 100))
```

    #> shape: (4, 2)
    #> ┌─────┬──────────┐
    #> │ a   ┆ replaced │
    #> │ --- ┆ ---      │
    #> │ f64 ┆ f64      │
    #> ╞═════╪══════════╡
    #> │ 1.0 ┆ 1.0      │
    #> │ 2.0 ┆ 100.0    │
    #> │ 2.0 ┆ 100.0    │
    #> │ 3.0 ┆ 3.0      │
    #> └─────┴──────────┘

``` r
df$with_columns(replaced = pl$col("a")$replace(c(2, 3), c(100, 200)))
```

    #> shape: (4, 2)
    #> ┌─────┬──────────┐
    #> │ a   ┆ replaced │
    #> │ --- ┆ ---      │
    #> │ f64 ┆ f64      │
    #> ╞═════╪══════════╡
    #> │ 1.0 ┆ 1.0      │
    #> │ 2.0 ┆ 100.0    │
    #> │ 2.0 ┆ 100.0    │
    #> │ 3.0 ┆ 200.0    │
    #> └─────┴──────────┘

``` r
# "old" can be a named list where names are values to replace, and values are
# the replacements
mapping = list(`2` = 100, `3` = 200)
df$with_columns(replaced = pl$col("a")$replace(mapping, default = -1))
```

    #> shape: (4, 2)
    #> ┌─────┬──────────┐
    #> │ a   ┆ replaced │
    #> │ --- ┆ ---      │
    #> │ f64 ┆ f64      │
    #> ╞═════╪══════════╡
    #> │ 1.0 ┆ -1.0     │
    #> │ 2.0 ┆ 100.0    │
    #> │ 2.0 ┆ 100.0    │
    #> │ 3.0 ┆ 200.0    │
    #> └─────┴──────────┘

``` r
df = pl$DataFrame(a = c("x", "y", "z"))
mapping = list(x = 1, y = 2, z = 3)
df$with_columns(replaced = pl$col("a")$replace(mapping))
```

    #> shape: (3, 2)
    #> ┌─────┬──────────┐
    #> │ a   ┆ replaced │
    #> │ --- ┆ ---      │
    #> │ str ┆ str      │
    #> ╞═════╪══════════╡
    #> │ x   ┆ 1.0      │
    #> │ y   ┆ 2.0      │
    #> │ z   ┆ 3.0      │
    #> └─────┴──────────┘

``` r
# one can specify the data type to return instead of automatically inferring it
df$with_columns(replaced = pl$col("a")$replace(mapping, return_dtype = pl$Int8))
```

    #> shape: (3, 2)
    #> ┌─────┬──────────┐
    #> │ a   ┆ replaced │
    #> │ --- ┆ ---      │
    #> │ str ┆ i8       │
    #> ╞═════╪══════════╡
    #> │ x   ┆ 1        │
    #> │ y   ┆ 2        │
    #> │ z   ┆ 3        │
    #> └─────┴──────────┘

``` r
# "old", "new", and "default" can take Expr
df = pl$DataFrame(a = c(1, 2, 2, 3), b = c(1.5, 2.5, 5, 1))
df$with_columns(
  replaced = pl$col("a")$replace(
    old = pl$col("a")$max(),
    new = pl$col("b")$sum(),
    default = pl$col("b"),
  )
)
```

    #> shape: (4, 3)
    #> ┌─────┬─────┬──────────┐
    #> │ a   ┆ b   ┆ replaced │
    #> │ --- ┆ --- ┆ ---      │
    #> │ f64 ┆ f64 ┆ f64      │
    #> ╞═════╪═════╪══════════╡
    #> │ 1.0 ┆ 1.5 ┆ 1.5      │
    #> │ 2.0 ┆ 2.5 ┆ 2.5      │
    #> │ 2.0 ┆ 5.0 ┆ 5.0      │
    #> │ 3.0 ┆ 1.0 ┆ 10.0     │
    #> └─────┴─────┴──────────┘
