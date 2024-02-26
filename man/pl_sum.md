

# Sum all values.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L405)

## Description

Syntactic sugar for <code>pl$col(…)$sum()</code>.

## Usage

<pre><code class='language-R'>pl_sum(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_sum_:_...">…</code>
</td>
<td>
Characters indicating the column names, passed to <code>pl$col()</code>.
See <code>?pl_col</code> for details.
</td>
</tr>
</table>

## Value

Expr

## See Also

<ul>
<li>

<code>\<Expr\>$sum()</code>

</li>
<li>

<code>pl$sum_horizontal()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(col_a = 1:2, col_b = 3:4, c = 5:6)

df$select(pl$sum("col_a"))
```

    #> shape: (1, 1)
    #> ┌───────┐
    #> │ col_a │
    #> │ ---   │
    #> │ i32   │
    #> ╞═══════╡
    #> │ 3     │
    #> └───────┘

``` r
# Sum multiple columns
df$select(pl$sum("col_a", "col_b"))
```

    #> shape: (1, 2)
    #> ┌───────┬───────┐
    #> │ col_a ┆ col_b │
    #> │ ---   ┆ ---   │
    #> │ i32   ┆ i32   │
    #> ╞═══════╪═══════╡
    #> │ 3     ┆ 7     │
    #> └───────┴───────┘

``` r
df$select(pl$sum("^col_.*$"))
```

    #> shape: (1, 2)
    #> ┌───────┬───────┐
    #> │ col_a ┆ col_b │
    #> │ ---   ┆ ---   │
    #> │ i32   ┆ i32   │
    #> ╞═══════╪═══════╡
    #> │ 3     ┆ 7     │
    #> └───────┴───────┘
