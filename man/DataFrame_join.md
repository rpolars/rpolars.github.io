

# Join DataFrames

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L946)

## Description

This function can do both mutating joins (adding columns based on
matching observations, for example with <code>how = “left”</code>) and
filtering joins (keeping observations based on matching observations,
for example with <code>how = “inner”</code>).

## Usage

<pre><code class='language-R'>DataFrame_join(
  other,
  on = NULL,
  how = c("inner", "left", "outer", "semi", "anti", "cross", "outer_coalesce"),
  ...,
  left_on = NULL,
  right_on = NULL,
  suffix = "_right",
  validate = "m:m",
  join_nulls = FALSE,
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
DataFrame to join with.
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
"cross", "outer_coalesce".
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_...">…</code>
</td>
<td>
Ignored.
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
<code id="DataFrame_join_:_suffix">suffix</code>
</td>
<td>
Suffix to add to duplicated column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_validate">validate</code>
</td>
<td>

Checks if join is of specified type:

<ul>
<li>

<code>“m:m”</code> (default): many-to-many, doesn’t perform any checks;

</li>
<li>

<code>“1:1”</code>: one-to-one, check if join keys are unique in both
left and right datasets;

</li>
<li>

<code>“1:m”</code>: one-to-many, check if join keys are unique in left
dataset

</li>
<li>

<code>“m:1”</code>: many-to-one, check if join keys are unique in right
dataset

</li>
</ul>
Note that this is currently not supported by the streaming engine, and
is only supported when joining by single columns.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_join_nulls">join_nulls</code>
</td>
<td>
Join on null values. By default null values will never produce matches.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_allow_parallel">allow_parallel</code>
</td>
<td>
Allow the physical plan to optionally evaluate the computation of both
DataFrames up to the join in parallel.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_:_force_parallel">force_parallel</code>
</td>
<td>
Force the physical plan to evaluate the computation of both DataFrames
up to the join in parallel.
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
    #> │ b   ┆ 1   │
    #> │ …   ┆ …   │
    #> │ b   ┆ 4   │
    #> │ c   ┆ 1   │
    #> │ c   ┆ 2   │
    #> │ c   ┆ 3   │
    #> │ c   ┆ 4   │
    #> └─────┴─────┘
