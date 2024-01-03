
# Add a prefix to a column name

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__name.R#L36)

## Description

Add a prefix to a column name

## Usage

<pre><code class='language-R'>ExprName_prefix(prefix)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprName_prefix_:_prefix">prefix</code>
</td>
<td>
Prefix to be added to column name(s)
</td>
</tr>
</table>

## Value

Expr

## See Also

<code>$suffix()</code> to add a suffix

## Examples

``` r
library(polars)

dat = pl$DataFrame(mtcars)

dat$select(
  pl$col("mpg"),
  pl$col("mpg")$name$prefix("name_"),
  pl$col("cyl", "drat")$name$prefix("bar_")
)
```

    #> shape: (32, 4)
    #> ┌──────┬──────────┬─────────┬──────────┐
    #> │ mpg  ┆ name_mpg ┆ bar_cyl ┆ bar_drat │
    #> │ ---  ┆ ---      ┆ ---     ┆ ---      │
    #> │ f64  ┆ f64      ┆ f64     ┆ f64      │
    #> ╞══════╪══════════╪═════════╪══════════╡
    #> │ 21.0 ┆ 21.0     ┆ 6.0     ┆ 3.9      │
    #> │ 21.0 ┆ 21.0     ┆ 6.0     ┆ 3.9      │
    #> │ 22.8 ┆ 22.8     ┆ 4.0     ┆ 3.85     │
    #> │ 21.4 ┆ 21.4     ┆ 6.0     ┆ 3.08     │
    #> │ …    ┆ …        ┆ …       ┆ …        │
    #> │ 15.8 ┆ 15.8     ┆ 8.0     ┆ 4.22     │
    #> │ 19.7 ┆ 19.7     ┆ 6.0     ┆ 3.62     │
    #> │ 15.0 ┆ 15.0     ┆ 8.0     ┆ 3.54     │
    #> │ 21.4 ┆ 21.4     ┆ 4.0     ┆ 4.11     │
    #> └──────┴──────────┴─────────┴──────────┘
