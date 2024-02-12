

# Cast an Expr to its physical representation

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

The following DataTypes will be converted:

<ul>
<li>

Date -\> Int32

</li>
<li>

Datetime -\> Int64

</li>
<li>

Time -\> Int64

</li>
<li>

Duration -\> Int64

</li>
<li>

Categorical -\> UInt32

</li>
<li>

List(inner) -\> List(physical of inner) Other data types will be left
unchanged.

</li>
</ul>

## Usage

<pre><code class='language-R'>Expr_to_physical()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(
  list(vals = c("a", "x", NA, "a", "b"))
)$with_columns(
  pl$col("vals")$cast(pl$Categorical),
  pl$col("vals")
  $cast(pl$Categorical)
  $to_physical()
  $alias("vals_physical")
)
```

    #> shape: (5, 2)
    #> ┌──────┬───────────────┐
    #> │ vals ┆ vals_physical │
    #> │ ---  ┆ ---           │
    #> │ cat  ┆ u32           │
    #> ╞══════╪═══════════════╡
    #> │ a    ┆ 0             │
    #> │ x    ┆ 1             │
    #> │ null ┆ null          │
    #> │ a    ┆ 0             │
    #> │ b    ┆ 2             │
    #> └──────┴───────────────┘
