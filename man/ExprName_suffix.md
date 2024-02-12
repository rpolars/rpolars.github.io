

# Add a suffix to a column name

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/expr__name.R#L16)

## Description

Add a suffix to a column name

## Usage

<pre><code class='language-R'>ExprName_suffix(suffix)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprName_suffix_:_suffix">suffix</code>
</td>
<td>
Suffix to be added to column name(s)
</td>
</tr>
</table>

## Value

Expr

## See Also

<code>$prefix()</code> to add a prefix

## Examples

``` r
library(polars)

dat = pl$DataFrame(mtcars)

dat$select(
  pl$col("mpg"),
  pl$col("mpg")$name$suffix("_foo"),
  pl$col("cyl", "drat")$name$suffix("_bar")
)
```

    #> shape: (32, 4)
    #> ┌──────┬─────────┬─────────┬──────────┐
    #> │ mpg  ┆ mpg_foo ┆ cyl_bar ┆ drat_bar │
    #> │ ---  ┆ ---     ┆ ---     ┆ ---      │
    #> │ f64  ┆ f64     ┆ f64     ┆ f64      │
    #> ╞══════╪═════════╪═════════╪══════════╡
    #> │ 21.0 ┆ 21.0    ┆ 6.0     ┆ 3.9      │
    #> │ 21.0 ┆ 21.0    ┆ 6.0     ┆ 3.9      │
    #> │ 22.8 ┆ 22.8    ┆ 4.0     ┆ 3.85     │
    #> │ 21.4 ┆ 21.4    ┆ 6.0     ┆ 3.08     │
    #> │ 18.7 ┆ 18.7    ┆ 8.0     ┆ 3.15     │
    #> │ …    ┆ …       ┆ …       ┆ …        │
    #> │ 30.4 ┆ 30.4    ┆ 4.0     ┆ 3.77     │
    #> │ 15.8 ┆ 15.8    ┆ 8.0     ┆ 4.22     │
    #> │ 19.7 ┆ 19.7    ┆ 6.0     ┆ 3.62     │
    #> │ 15.0 ┆ 15.0    ┆ 8.0     ┆ 3.54     │
    #> │ 21.4 ┆ 21.4    ┆ 4.0     ┆ 4.11     │
    #> └──────┴─────────┴─────────┴──────────┘
