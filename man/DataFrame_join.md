
# Join DataFrames

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L921)

## Description

This function can do both mutating joins (adding columns based on
matching observations, for example with <code>how = “left”</code>) and
filtering joins (keeping observations based on matching observations,
for example with <code>how = “inner”</code>).

## Usage

<pre><code class='language-R'>DataFrame_join(
  other,
  left_on = NULL,
  right_on = NULL,
  on = NULL,
  how = c("inner", "left", "outer", "semi", "anti", "cross"),
  suffix = "_right",
  allow_parallel = TRUE,
  force_parallel = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_other">other</code>
</td>
<td>
DataFrame
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_left_on">left_on</code>,
<code id="DataFrame_join_:_right_on">right_on</code>
</td>
<td>
Same as <code>on</code> but only for the left or the right DataFrame.
They must have the same length.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_on">on</code>
</td>
<td>
Either a vector of column names or a list of expressions and/or strings.
Use <code>left_on</code> and <code>right_on</code> if the column names
to match on are different between the two DataFrames.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_how">how</code>
</td>
<td>
One of the following methods: "inner", "left", "outer", "semi", "anti",
"cross".
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_suffix">suffix</code>
</td>
<td>
Suffix to add to duplicated column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_allow_parallel">allow_parallel</code>
</td>
<td>
Boolean.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_force_parallel">force_parallel</code>
</td>
<td>
Boolean.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

# inner join by default
df1 = pl$DataFrame(list(key = 1:3, payload = c("f", "i", NA)))
df2 = pl$DataFrame(list(key = c(3L, 4L, 5L, NA_integer_)))
df1$join(other = df2, on = "key")
```

    #> shape: (1, 2)
    #> ┌─────┬─────────┐
    #> │ key ┆ payload │
    #> │ --- ┆ ---     │
    #> │ i32 ┆ str     │
    #> ╞═════╪═════════╡
    #> │ 3   ┆ null    │
    #> └─────┴─────────┘

``` r
# cross join
df1 = pl$DataFrame(x = letters[1:3])
df2 = pl$DataFrame(y = 1:4)
df1$join(other = df2, how = "cross")
```

    #> shape: (12, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ y   │
    #> │ --- ┆ --- │
    #> │ str ┆ i32 │
    #> ╞═════╪═════╡
    #> │ a   ┆ 1   │
    #> │ a   ┆ 2   │
    #> │ a   ┆ 3   │
    #> │ a   ┆ 4   │
    #> │ …   ┆ …   │
    #> │ c   ┆ 1   │
    #> │ c   ┆ 2   │
    #> │ c   ┆ 3   │
    #> │ c   ┆ 4   │
    #> └─────┴─────┘
