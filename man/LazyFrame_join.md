

# Join LazyFrames

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/lazyframe__lazy.R#L1210)

## Description

This function can do both mutating joins (adding columns based on
matching observations, for example with <code>how = “left”</code>) and
filtering joins (keeping observations based on matching observations,
for example with <code>how = “inner”</code>).

## Usage

<pre><code class='language-R'>LazyFrame_join(
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
<code id="LazyFrame_join_:_other">other</code>
</td>
<td>
LazyFrame to join with.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_join_:_on">on</code>
</td>
<td>
Either a vector of column names or a list of expressions and/or strings.
Use <code>left_on</code> and <code>right_on</code> if the column names
to match on are different between the two DataFrames.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_join_:_how">how</code>
</td>
<td>
One of the following methods: "inner", "left", "outer", "semi", "anti",
"cross", "outer_coalesce".
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_join_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_join_:_left_on">left_on</code>,
<code id="LazyFrame_join_:_right_on">right_on</code>
</td>
<td>
Same as <code>on</code> but only for the left or the right DataFrame.
They must have the same length.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_join_:_suffix">suffix</code>
</td>
<td>
Suffix to add to duplicated column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_join_:_validate">validate</code>
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
<code id="LazyFrame_join_:_join_nulls">join_nulls</code>
</td>
<td>
Join on null values. By default null values will never produce matches.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_join_:_allow_parallel">allow_parallel</code>
</td>
<td>
Allow the physical plan to optionally evaluate the computation of both
DataFrames up to the join in parallel.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_join_:_force_parallel">force_parallel</code>
</td>
<td>
Force the physical plan to evaluate the computation of both DataFrames
up to the join in parallel.
</td>
</tr>
</table>

## Value

LazyFrame

## Examples

``` r
library(polars)

# inner join by default
df1 = pl$LazyFrame(list(key = 1:3, payload = c("f", "i", NA)))
df2 = pl$LazyFrame(list(key = c(3L, 4L, 5L, NA_integer_)))
df1$join(other = df2, on = "key")
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> INNER JOIN:
    #> LEFT PLAN ON: [col("key")]
    #>   DF ["key", "payload"]; PROJECT */2 COLUMNS; SELECTION: "None"
    #> RIGHT PLAN ON: [col("key")]
    #>   DF ["key"]; PROJECT */1 COLUMNS; SELECTION: "None"
    #> END INNER JOIN

``` r
# cross join
df1 = pl$LazyFrame(x = letters[1:3])
df2 = pl$LazyFrame(y = 1:4)
df1$join(other = df2, how = "cross")
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> CROSS JOIN:
    #> LEFT PLAN ON: [col("x")]
    #>   DF ["x"]; PROJECT */1 COLUMNS; SELECTION: "None"
    #> RIGHT PLAN ON: [col("y")]
    #>   DF ["y"]; PROJECT */1 COLUMNS; SELECTION: "None"
    #> END CROSS JOIN

``` r
# use "validate" to ensure join keys are not duplicated
df1 = pl$LazyFrame(x = letters[1:5], y = 1:5)
df2 = pl$LazyFrame(x = c("a", letters[1:4]), y2 = 6:10)

# this throws an error because there are two keys in df2 that match the key
# in df1
tryCatch(
  df1$join(df2, on = "x", validate = "1:1")$collect(),
  error = function(e) print(e)
)
```

    #> <RPolarsErr_error: Execution halted with the following contexts
    #>    0: In R: in $collect():
    #>    0: During function call [.main()]
    #>    1: Encountered the following error in Rust-Polars:
    #>          the join keys did not fulfil 1:1 validation
    #> >
