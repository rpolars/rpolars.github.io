

# Explode columns containing a list of values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1710)

## Description

Explode columns containing a list of values

## Usage

<pre><code class='language-R'>DataFrame_explode(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_explode_:_...">…</code>
</td>
<td>
Column(s) to be exploded as individual
<code style="white-space: pre;">Into\<Expr\></code> or list/vector of
<code style="white-space: pre;">Into\<Expr\></code>. In a handful of
places in rust-polars, only the plain variant <code>Expr::Column</code>
is accepted. This is currenly one of such places. Therefore
<code>pl$col(“name”)</code> and <code>pl$all()</code> is allowed, not
<code>pl$col(“name”)$alias(“newname”)</code>. <code>“name”</code> is
implicitly converted to <code>pl$col(“name”)</code>.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  letters = letters[1:4],
  numbers = list(1, c(2, 3), c(4, 5), c(6, 7, 8)),
  numbers_2 = list(0, c(1, 2), c(3, 4), c(5, 6, 7)) # same structure as numbers
)
df
```

    #> shape: (4, 3)
    #> ┌─────────┬─────────────────┬─────────────────┐
    #> │ letters ┆ numbers         ┆ numbers_2       │
    #> │ ---     ┆ ---             ┆ ---             │
    #> │ str     ┆ list[f64]       ┆ list[f64]       │
    #> ╞═════════╪═════════════════╪═════════════════╡
    #> │ a       ┆ [1.0]           ┆ [0.0]           │
    #> │ b       ┆ [2.0, 3.0]      ┆ [1.0, 2.0]      │
    #> │ c       ┆ [4.0, 5.0]      ┆ [3.0, 4.0]      │
    #> │ d       ┆ [6.0, 7.0, 8.0] ┆ [5.0, 6.0, 7.0] │
    #> └─────────┴─────────────────┴─────────────────┘

``` r
# explode a single column, append others
df$explode("numbers")
```

    #> shape: (8, 3)
    #> ┌─────────┬─────────┬─────────────────┐
    #> │ letters ┆ numbers ┆ numbers_2       │
    #> │ ---     ┆ ---     ┆ ---             │
    #> │ str     ┆ f64     ┆ list[f64]       │
    #> ╞═════════╪═════════╪═════════════════╡
    #> │ a       ┆ 1.0     ┆ [0.0]           │
    #> │ b       ┆ 2.0     ┆ [1.0, 2.0]      │
    #> │ b       ┆ 3.0     ┆ [1.0, 2.0]      │
    #> │ c       ┆ 4.0     ┆ [3.0, 4.0]      │
    #> │ c       ┆ 5.0     ┆ [3.0, 4.0]      │
    #> │ d       ┆ 6.0     ┆ [5.0, 6.0, 7.0] │
    #> │ d       ┆ 7.0     ┆ [5.0, 6.0, 7.0] │
    #> │ d       ┆ 8.0     ┆ [5.0, 6.0, 7.0] │
    #> └─────────┴─────────┴─────────────────┘

``` r
# explode two columns of same nesting structure, by names or the common dtype
# "List(Float64)"
df$explode("numbers", "numbers_2")
```

    #> shape: (8, 3)
    #> ┌─────────┬─────────┬───────────┐
    #> │ letters ┆ numbers ┆ numbers_2 │
    #> │ ---     ┆ ---     ┆ ---       │
    #> │ str     ┆ f64     ┆ f64       │
    #> ╞═════════╪═════════╪═══════════╡
    #> │ a       ┆ 1.0     ┆ 0.0       │
    #> │ b       ┆ 2.0     ┆ 1.0       │
    #> │ b       ┆ 3.0     ┆ 2.0       │
    #> │ c       ┆ 4.0     ┆ 3.0       │
    #> │ c       ┆ 5.0     ┆ 4.0       │
    #> │ d       ┆ 6.0     ┆ 5.0       │
    #> │ d       ┆ 7.0     ┆ 6.0       │
    #> │ d       ┆ 8.0     ┆ 7.0       │
    #> └─────────┴─────────┴───────────┘

``` r
df$explode(pl$col(pl$List(pl$Float64)))
```

    #> shape: (8, 3)
    #> ┌─────────┬─────────┬───────────┐
    #> │ letters ┆ numbers ┆ numbers_2 │
    #> │ ---     ┆ ---     ┆ ---       │
    #> │ str     ┆ f64     ┆ f64       │
    #> ╞═════════╪═════════╪═══════════╡
    #> │ a       ┆ 1.0     ┆ 0.0       │
    #> │ b       ┆ 2.0     ┆ 1.0       │
    #> │ b       ┆ 3.0     ┆ 2.0       │
    #> │ c       ┆ 4.0     ┆ 3.0       │
    #> │ c       ┆ 5.0     ┆ 4.0       │
    #> │ d       ┆ 6.0     ┆ 5.0       │
    #> │ d       ┆ 7.0     ┆ 6.0       │
    #> │ d       ┆ 8.0     ┆ 7.0       │
    #> └─────────┴─────────┴───────────┘
