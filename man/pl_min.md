

# Get the minimum value.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L457)

## Description

Syntactic sugar for <code>pl$col(…)$min()</code>.

## Usage

<pre><code class='language-R'>pl_min(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_min_:_...">…</code>
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

<code>\<Expr\>$min()</code>

</li>
<li>

<code>pl$min_horizontal()</code>

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

df$select(pl$min("num_1"))
```

    #> shape: (1, 1)
    #> ┌───────┐
    #> │ num_1 │
    #> │ ---   │
    #> │ f64   │
    #> ╞═══════╡
    #> │ 1.0   │
    #> └───────┘

``` r
# Get the minimum value of multiple columns.
df$select(pl$min(r"(^num_\d+$)"))
```

    #> shape: (1, 2)
    #> ┌───────┬───────┐
    #> │ num_1 ┆ num_2 │
    #> │ ---   ┆ ---   │
    #> │ f64   ┆ f64   │
    #> ╞═══════╪═══════╡
    #> │ 1.0   ┆ 2.0   │
    #> └───────┴───────┘

``` r
df$select(pl$min("num_1", "num_2"))
```

    #> shape: (1, 2)
    #> ┌───────┬───────┐
    #> │ num_1 ┆ num_2 │
    #> │ ---   ┆ ---   │
    #> │ f64   ┆ f64   │
    #> ╞═══════╪═══════╡
    #> │ 1.0   ┆ 2.0   │
    #> └───────┴───────┘
