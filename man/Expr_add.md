

# Add two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L229)

## Description

Method equivalent of addition operator <code>expr + other</code>.

## Usage

<pre><code class='language-R'>Expr_add(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="other">other</code>
</td>
<td>
numeric or string value; accepts expression input.
</td>
</tr>
</table>

## Value

Expr

## See Also

<ul>
<li>

Arithmetic operators

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(x = 1:5)

df$with_columns(
  `x+int` = pl$col("x")$add(2L),
  `x+expr` = pl$col("x")$add(pl$col("x")$cum_prod())
)
```

    #> shape: (5, 3)
    #> ┌─────┬───────┬────────┐
    #> │ x   ┆ x+int ┆ x+expr │
    #> │ --- ┆ ---   ┆ ---    │
    #> │ i32 ┆ i32   ┆ i64    │
    #> ╞═════╪═══════╪════════╡
    #> │ 1   ┆ 3     ┆ 2      │
    #> │ 2   ┆ 4     ┆ 4      │
    #> │ 3   ┆ 5     ┆ 9      │
    #> │ 4   ┆ 6     ┆ 28     │
    #> │ 5   ┆ 7     ┆ 125    │
    #> └─────┴───────┴────────┘

``` r
df = pl$DataFrame(
  x = c("a", "d", "g"),
  y = c("b", "e", "h"),
  z = c("c", "f", "i")
)

df$with_columns(
  pl$col("x")$add(pl$col("y"))$add(pl$col("z"))$alias("xyz")
)
```

    #> shape: (3, 4)
    #> ┌─────┬─────┬─────┬─────┐
    #> │ x   ┆ y   ┆ z   ┆ xyz │
    #> │ --- ┆ --- ┆ --- ┆ --- │
    #> │ str ┆ str ┆ str ┆ str │
    #> ╞═════╪═════╪═════╪═════╡
    #> │ a   ┆ b   ┆ c   ┆ abc │
    #> │ d   ┆ e   ┆ f   ┆ def │
    #> │ g   ┆ h   ┆ i   ┆ ghi │
    #> └─────┴─────┴─────┴─────┘
