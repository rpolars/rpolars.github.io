

# Configure optimization toggles

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L419)

## Description

Configure the optimization toggles for the lazy query

## Usage

<pre><code class='language-R'>LazyFrame_set_optimization_toggle(
  type_coercion = TRUE,
  predicate_pushdown = TRUE,
  projection_pushdown = TRUE,
  simplify_expression = TRUE,
  slice_pushdown = TRUE,
  comm_subplan_elim = TRUE,
  comm_subexpr_elim = TRUE,
  streaming = FALSE,
  eager = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="type_coercion">type_coercion</code>
</td>
<td>
Logical. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Logical. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="projection_pushdown">projection_pushdown</code>
</td>
<td>
Logical. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="simplify_expression">simplify_expression</code>
</td>
<td>
Logical. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="slice_pushdown">slice_pushdown</code>
</td>
<td>
Logical. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="comm_subplan_elim">comm_subplan_elim</code>
</td>
<td>
Logical. Will try to cache branching subplans that occur on self-joins
or unions.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="comm_subexpr_elim">comm_subexpr_elim</code>
</td>
<td>
Logical. Common subexpressions will be cached and reused.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="streaming">streaming</code>
</td>
<td>
Logical. Run parts of the query in a streaming fashion (this is in an
alpha state).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="eager">eager</code>
</td>
<td>
Logical. Run the query eagerly.
</td>
</tr>
</table>

## Value

LazyFrame with specified optimization toggles

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$set_optimization_toggle(type_coercion = FALSE)
```

    #> $ok
    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
    #> 
    #> $err
    #> NULL
    #> 
    #> attr(,"class")
    #> [1] "extendr_result"
