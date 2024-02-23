

# Create new LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/lazyframe__lazy.R#L195)

## Description

This is simply a convenience function to create <code>LazyFrame</code>s
in a quick way. It is a wrapper around
<code>pl$DataFrame()$lazy()</code>. Note that this should only be used
for making examples and quick demonstrations.

## Usage

<pre><code class='language-R'>pl_LazyFrame(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_LazyFrame_:_...">…</code>
</td>
<td>
Anything that is accepted by <code>pl$DataFrame()</code>
</td>
</tr>
</table>

## Value

LazyFrame

## Examples

``` r
library(polars)

pl$LazyFrame(
  a = list(c(1, 2, 3, 4, 5)),
  b = 1:5,
  c = letters[1:5],
  d = list(1:1, 1:2, 1:3, 1:4, 1:5)
) # directly from vectors
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> DF ["a", "b", "c", "d"]; PROJECT */4 COLUMNS; SELECTION: "None"

``` r
# from a list of vectors or data.frame
pl$LazyFrame(list(
  a = c(1, 2, 3, 4, 5),
  b = 1:5,
  c = letters[1:5],
  d = list(1L, 1:2, 1:3, 1:4, 1:5)
))
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> DF ["a", "b", "c", "d"]; PROJECT */4 COLUMNS; SELECTION: "None"

``` r
# custom schema
pl$LazyFrame(
  iris,
  schema = list(Sepal.Length = pl$Float32, Species = pl$String)
)$collect()
```

    #> shape: (150, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       │
    #> │ f32          ┆ f64         ┆ f64          ┆ f64         ┆ str       │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa    │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa    │
    #> │ 5.0          ┆ 3.6         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …         │
    #> │ 6.7          ┆ 3.0         ┆ 5.2          ┆ 2.3         ┆ virginica │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         ┆ virginica │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         ┆ virginica │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┘
