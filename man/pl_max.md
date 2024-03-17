

# Get the maximum value.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L483)

## Description

Syntactic sugar for <code>pl$col(…)$max()</code>.

## Usage

<pre><code class='language-R'>pl_max(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_max_:_...">…</code>
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

<code>\<Expr\>$max()</code>

</li>
<li>

<code>pl$max_horizontal()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  num_1 = c(1, 8, 3),
  num_2 = c(4, 5, 2),
  chr_1 = c("foo", "bar", "foo")
)

df$select(pl$max("num_1"))
```

    #> shape: (1, 1)
    #> ┌───────┐
    #> │ num_1 │
    #> │ ---   │
    #> │ f64   │
    #> ╞═══════╡
    #> │ 8.0   │
    #> └───────┘

``` r
# Get the maximum value of multiple columns.
df$select(pl$max(r"(^num_\d+$)"))
```

    #> shape: (1, 2)
    #> ┌───────┬───────┐
    #> │ num_1 ┆ num_2 │
    #> │ ---   ┆ ---   │
    #> │ f64   ┆ f64   │
    #> ╞═══════╪═══════╡
    #> │ 8.0   ┆ 5.0   │
    #> └───────┴───────┘

``` r
df$select(pl$max("num_1", "num_2"))
```

    #> shape: (1, 2)
    #> ┌───────┬───────┐
    #> │ num_1 ┆ num_2 │
    #> │ ---   ┆ ---   │
    #> │ f64   ┆ f64   │
    #> ╞═══════╪═══════╡
    #> │ 8.0   ┆ 5.0   │
    #> └───────┴───────┘
