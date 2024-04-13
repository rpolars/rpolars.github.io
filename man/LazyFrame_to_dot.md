

# Plot the query plan

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L2023)

## Description

This only returns the "dot" output that can be passed to other packages,
such as <code>DiagrammeR::grViz()</code>.

## Usage

<pre><code class='language-R'>LazyFrame_to_dot(
  ...,
  optimized = TRUE,
  type_coercion = TRUE,
  predicate_pushdown = TRUE,
  projection_pushdown = TRUE,
  simplify_expression = TRUE,
  slice_pushdown = TRUE,
  comm_subplan_elim = TRUE,
  comm_subexpr_elim = TRUE,
  streaming = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_...">…</code>
</td>
<td>
Not used..
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_optimized">optimized</code>
</td>
<td>
Optimize the query plan.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_type_coercion">type_coercion</code>
</td>
<td>
Logical. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Logical. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_projection_pushdown">projection_pushdown</code>
</td>
<td>
Logical. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_simplify_expression">simplify_expression</code>
</td>
<td>
Logical. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_slice_pushdown">slice_pushdown</code>
</td>
<td>
Logical. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_comm_subplan_elim">comm_subplan_elim</code>
</td>
<td>
Logical. Will try to cache branching subplans that occur on self-joins
or unions.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_comm_subexpr_elim">comm_subexpr_elim</code>
</td>
<td>
Logical. Common subexpressions will be cached and reused.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_to_dot_:_streaming">streaming</code>
</td>
<td>
Logical. Run parts of the query in a streaming fashion (this is in an
alpha state).
</td>
</tr>
</table>

## Value

A character vector

## Examples

``` r
library(polars)

lf = pl$LazyFrame(
  a = c("a", "b", "a", "b", "b", "c"),
  b = 1:6,
  c = 6:1
)

query = lf$group_by("a", maintain_order = TRUE)$agg(
  pl$all()$sum()
)$sort(
  "a"
)

query$to_dot() |> cat()
```

    #> graph  polars_query {
    #> "SORT BY [col(\"a\")] [(0, 0)]" -- "AGG [col(\"b\").sum(), col(\"c\").sum()]
    #> BY
    #> [col(\"a\")] [(0, 1)] [(0, 1)]"
    #> "AGG [col(\"b\").sum(), col(\"c\").sum()]
    #> BY
    #> [col(\"a\")] [(0, 1)] [(0, 1)]" -- "TABLE
    #> π 3/3;
    #> σ - [(0, 2)]"
    #> 
    #> "SORT BY [col(\"a\")] [(0, 0)]"[label="SORT BY [col(\"a\")]"]
    #> "TABLE
    #> π 3/3;
    #> σ - [(0, 2)]"[label="TABLE
    #> π 3/3;
    #> σ -"]
    #> "AGG [col(\"b\").sum(), col(\"c\").sum()]
    #> BY
    #> [col(\"a\")] [(0, 1)] [(0, 1)]"[label="AGG [col(\"b\").sum(), col(\"c\").sum()]
    #> BY
    #> [col(\"a\")] [(0, 1)]"]
    #> 
    #> }

``` r
# You could print the graph by using DiagrammeR for example, with
# query$to_dot() |> DiagrammeR::grViz().
```
