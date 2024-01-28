

# Select from an empty DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L302)

## Description

<code>pl$select(…)</code> is a shorthand for
<code>pl$DataFrame(list())$select(…)</code>

## Usage

<pre><code class='language-R'>pl_select(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_select_:_...">…</code>
</td>
<td>
Expressions
</td>
</tr>
</table>

## Value

a DataFrame

## Examples

``` r
library(polars)

pl$select(
  pl$lit(1:4)$alias("ints"),
  pl$lit(letters[1:4])$alias("letters")
)
```

    #> shape: (4, 2)
    #> ┌──────┬─────────┐
    #> │ ints ┆ letters │
    #> │ ---  ┆ ---     │
    #> │ i32  ┆ str     │
    #> ╞══════╪═════════╡
    #> │ 1    ┆ a       │
    #> │ 2    ┆ b       │
    #> │ 3    ┆ c       │
    #> │ 4    ┆ d       │
    #> └──────┴─────────┘
