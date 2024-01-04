
# Join LazyFrames

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/lazyframe__lazy.R#L1008)

## Description

This function can do both mutating joins (adding columns based on
matching observations, for example with <code>how = “left”</code>) and
filtering joins (keeping observations based on matching observations,
for example with <code>how = “inner”</code>).

## Usage

<pre><code class='language-R'>LazyFrame_join(
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
<code id="LazyFrame_join_:_other">other</code>
</td>
<td>
DataFrame
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
"cross".
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
<code id="LazyFrame_join_:_allow_parallel">allow_parallel</code>
</td>
<td>
Boolean.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_join_:_force_parallel">force_parallel</code>
</td>
<td>
Boolean.
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

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
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

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> CROSS JOIN:
    #> LEFT PLAN ON: [col("x")]
    #>   DF ["x"]; PROJECT */1 COLUMNS; SELECTION: "None"
    #> RIGHT PLAN ON: [col("y")]
    #>   DF ["y"]; PROJECT */1 COLUMNS; SELECTION: "None"
    #> END CROSS JOIN
