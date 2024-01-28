

# Shuffle values

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__expr.R#L2918)

## Description

Shuffle values

## Usage

<pre><code class='language-R'>Expr_shuffle(seed = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_shuffle_:_seed">seed</code>
</td>
<td>
numeric value of 0 to 2^52 Seed for the random number generator. If
<code>NULL</code> (default), a random seed value between 0 and 10000 is
picked.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = 1:4)$with_columns(shuff = pl$col("a")$shuffle(seed = 1))
```

    #> shape: (4, 2)
    #> ┌─────┬───────┐
    #> │ a   ┆ shuff │
    #> │ --- ┆ ---   │
    #> │ i32 ┆ i32   │
    #> ╞═════╪═══════╡
    #> │ 1   ┆ 2     │
    #> │ 2   ┆ 3     │
    #> │ 3   ┆ 4     │
    #> │ 4   ┆ 1     │
    #> └─────┴───────┘
