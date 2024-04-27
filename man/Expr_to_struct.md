

# Convert an Expr to a Struct

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L3209)

## Description

Convert an Expr to a Struct

## Usage

<pre><code class='language-R'>Expr_to_struct()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(iris[, 3:5])$with_columns(
  my_struct = pl$all()$to_struct()
)
```

    #> shape: (150, 4)
    #> ┌──────────────┬─────────────┬───────────┬───────────────────────┐
    #> │ Petal.Length ┆ Petal.Width ┆ Species   ┆ my_struct             │
    #> │ ---          ┆ ---         ┆ ---       ┆ ---                   │
    #> │ f64          ┆ f64         ┆ cat       ┆ struct[3]             │
    #> ╞══════════════╪═════════════╪═══════════╪═══════════════════════╡
    #> │ 1.4          ┆ 0.2         ┆ setosa    ┆ {1.4,0.2,"setosa"}    │
    #> │ 1.4          ┆ 0.2         ┆ setosa    ┆ {1.4,0.2,"setosa"}    │
    #> │ 1.3          ┆ 0.2         ┆ setosa    ┆ {1.3,0.2,"setosa"}    │
    #> │ 1.5          ┆ 0.2         ┆ setosa    ┆ {1.5,0.2,"setosa"}    │
    #> │ 1.4          ┆ 0.2         ┆ setosa    ┆ {1.4,0.2,"setosa"}    │
    #> │ …            ┆ …           ┆ …         ┆ …                     │
    #> │ 5.2          ┆ 2.3         ┆ virginica ┆ {5.2,2.3,"virginica"} │
    #> │ 5.0          ┆ 1.9         ┆ virginica ┆ {5.0,1.9,"virginica"} │
    #> │ 5.2          ┆ 2.0         ┆ virginica ┆ {5.2,2.0,"virginica"} │
    #> │ 5.4          ┆ 2.3         ┆ virginica ┆ {5.4,2.3,"virginica"} │
    #> │ 5.1          ┆ 1.8         ┆ virginica ┆ {5.1,1.8,"virginica"} │
    #> └──────────────┴─────────────┴───────────┴───────────────────────┘
