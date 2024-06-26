

# Take a sample

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2868)

## Description

Take a sample

## Usage

<pre><code class='language-R'>Expr_sample(
  frac = NULL,
  with_replacement = TRUE,
  shuffle = FALSE,
  seed = NULL,
  n = NULL
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="frac">frac</code>
</td>
<td>
Fraction of items to return (can be higher than 1). Cannot be used with
<code>n</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="with_replacement">with_replacement</code>
</td>
<td>
If <code>TRUE</code> (default), allow values to be sampled more than
once.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="shuffle">shuffle</code>
</td>
<td>
Shuffle the order of sampled data points (implicitly <code>TRUE</code>
if <code>with_replacement = TRUE</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="seed">seed</code>
</td>
<td>
numeric value of 0 to 2^52 Seed for the random number generator. If
<code>NULL</code> (default), a random seed value between 0 and 10000 is
picked.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
Number of items to return. Cannot be used with <code>frac</code>.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = 1:4)
df$select(pl$col("a")$sample(frac = 1, with_replacement = TRUE, seed = 1L))
```

    #> shape: (4, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 3   │
    #> │ 1   │
    #> │ 1   │
    #> │ 2   │
    #> └─────┘

``` r
df$select(pl$col("a")$sample(frac = 2, with_replacement = TRUE, seed = 1L))
```

    #> shape: (8, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 3   │
    #> │ 1   │
    #> │ 1   │
    #> │ 2   │
    #> │ 2   │
    #> │ 4   │
    #> │ 1   │
    #> │ 2   │
    #> └─────┘

``` r
df$select(pl$col("a")$sample(n = 2, with_replacement = FALSE, seed = 1L))
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 3   │
    #> │ 1   │
    #> └─────┘
