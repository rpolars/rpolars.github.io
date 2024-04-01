

# Unnest the Struct columns of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1133)

## Description

Unnest the Struct columns of a DataFrame

## Usage

<pre><code class='language-R'>DataFrame_unnest(names = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_unnest_:_names">names</code>
</td>
<td>
Names of the struct columns to unnest. If <code>NULL</code> (default),
then all "struct" columns are unnested.
</td>
</tr>
</table>

## Value

A DataFrame where all "struct" columns are unnested. Non-struct columns
are not modified.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = 1:5,
  b = c("one", "two", "three", "four", "five"),
  c = 6:10
)$
  select(
  pl$col("b")$to_struct(),
  pl$col("a", "c")$to_struct()$alias("a_and_c")
)
df
```

    #> shape: (5, 2)
    #> ┌───────────┬───────────┐
    #> │ b         ┆ a_and_c   │
    #> │ ---       ┆ ---       │
    #> │ struct[1] ┆ struct[2] │
    #> ╞═══════════╪═══════════╡
    #> │ {"one"}   ┆ {1,6}     │
    #> │ {"two"}   ┆ {2,7}     │
    #> │ {"three"} ┆ {3,8}     │
    #> │ {"four"}  ┆ {4,9}     │
    #> │ {"five"}  ┆ {5,10}    │
    #> └───────────┴───────────┘

``` r
# by default, all struct columns are unnested
df$unnest()
```

    #> shape: (5, 3)
    #> ┌───────┬─────┬─────┐
    #> │ b     ┆ a   ┆ c   │
    #> │ ---   ┆ --- ┆ --- │
    #> │ str   ┆ i32 ┆ i32 │
    #> ╞═══════╪═════╪═════╡
    #> │ one   ┆ 1   ┆ 6   │
    #> │ two   ┆ 2   ┆ 7   │
    #> │ three ┆ 3   ┆ 8   │
    #> │ four  ┆ 4   ┆ 9   │
    #> │ five  ┆ 5   ┆ 10  │
    #> └───────┴─────┴─────┘

``` r
# we can specify specific columns to unnest
df$unnest("a_and_c")
```

    #> shape: (5, 3)
    #> ┌───────────┬─────┬─────┐
    #> │ b         ┆ a   ┆ c   │
    #> │ ---       ┆ --- ┆ --- │
    #> │ struct[1] ┆ i32 ┆ i32 │
    #> ╞═══════════╪═════╪═════╡
    #> │ {"one"}   ┆ 1   ┆ 6   │
    #> │ {"two"}   ┆ 2   ┆ 7   │
    #> │ {"three"} ┆ 3   ┆ 8   │
    #> │ {"four"}  ┆ 4   ┆ 9   │
    #> │ {"five"}  ┆ 5   ┆ 10  │
    #> └───────────┴─────┴─────┘
