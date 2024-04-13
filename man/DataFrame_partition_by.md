

# Split a DataFrame into multiple DataFrames

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L2246)

## Description

Similar to <code>$group_by()</code>. Group by the given columns and
return the groups as separate DataFrames. It is useful to use this in
combination with functions like <code>lapply()</code> or
<code>purrr::map()</code>.

## Usage

<pre><code class='language-R'>DataFrame_partition_by(
  ...,
  maintain_order = TRUE,
  include_key = TRUE,
  as_nested_list = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_partition_by_:_...">…</code>
</td>
<td>
Characters of column names to group by. Passed to <code>pl$col()</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_partition_by_:_maintain_order">maintain_order</code>
</td>
<td>
If <code>TRUE</code>, ensure that the order of the groups is consistent
with the input data. This is slower than a default partition by
operation.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_partition_by_:_include_key">include_key</code>
</td>
<td>
If <code>TRUE</code>, include the columns used to partition the
DataFrame in the output.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_partition_by_:_as_nested_list">as_nested_list</code>
</td>
<td>
This affects the format of the output. If <code>FALSE</code> (default),
the output is a flat list of DataFrames. IF <code>TRUE</code> and one of
the <code>maintain_order</code> or <code>include_key</code> argument is
<code>TRUE</code>, then each element of the output has two children:
<code>key</code> and <code>data</code>. See the examples for more
details.
</td>
</tr>
</table>

## Value

A list of DataFrames. See the examples for details.

## See Also

<ul>
<li>

<code>\<DataFrame\>$group_by()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c("a", "b", "a", "b", "c"),
  b = c(1, 2, 1, 3, 3),
  c = c(5, 4, 3, 2, 1)
)
df
```

    #> shape: (5, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ a   ┆ 1.0 ┆ 5.0 │
    #> │ b   ┆ 2.0 ┆ 4.0 │
    #> │ a   ┆ 1.0 ┆ 3.0 │
    #> │ b   ┆ 3.0 ┆ 2.0 │
    #> │ c   ┆ 3.0 ┆ 1.0 │
    #> └─────┴─────┴─────┘

``` r
# Pass a single column name to partition by that column.
df$partition_by("a")
```

    #> [[1]]
    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ a   ┆ 1.0 ┆ 5.0 │
    #> │ a   ┆ 1.0 ┆ 3.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> [[2]]
    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ b   ┆ 2.0 ┆ 4.0 │
    #> │ b   ┆ 3.0 ┆ 2.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> [[3]]
    #> shape: (1, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ c   ┆ 3.0 ┆ 1.0 │
    #> └─────┴─────┴─────┘

``` r
# Partition by multiple columns.
df$partition_by("a", "b")
```

    #> [[1]]
    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ a   ┆ 1.0 ┆ 5.0 │
    #> │ a   ┆ 1.0 ┆ 3.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> [[2]]
    #> shape: (1, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ b   ┆ 2.0 ┆ 4.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> [[3]]
    #> shape: (1, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ b   ┆ 3.0 ┆ 2.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> [[4]]
    #> shape: (1, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ c   ┆ 3.0 ┆ 1.0 │
    #> └─────┴─────┴─────┘

``` r
# Partition by column data type
df$partition_by(pl$String)
```

    #> [[1]]
    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ a   ┆ 1.0 ┆ 5.0 │
    #> │ a   ┆ 1.0 ┆ 3.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> [[2]]
    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ b   ┆ 2.0 ┆ 4.0 │
    #> │ b   ┆ 3.0 ┆ 2.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> [[3]]
    #> shape: (1, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ c   ┆ 3.0 ┆ 1.0 │
    #> └─────┴─────┴─────┘

``` r
# If `as_nested_list = TRUE`, the output is a list whose elements have a `key` and a `data` field.
# The `key` is a named list of the key values, and the `data` is the DataFrame.
df$partition_by("a", "b", as_nested_list = TRUE)
```

    #> [[1]]
    #> [[1]]$key
    #> [[1]]$key$a
    #> [1] "a"
    #> 
    #> [[1]]$key$b
    #> [1] 1
    #> 
    #> 
    #> [[1]]$data
    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ a   ┆ 1.0 ┆ 5.0 │
    #> │ a   ┆ 1.0 ┆ 3.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> 
    #> [[2]]
    #> [[2]]$key
    #> [[2]]$key$a
    #> [1] "b"
    #> 
    #> [[2]]$key$b
    #> [1] 2
    #> 
    #> 
    #> [[2]]$data
    #> shape: (1, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ b   ┆ 2.0 ┆ 4.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> 
    #> [[3]]
    #> [[3]]$key
    #> [[3]]$key$a
    #> [1] "b"
    #> 
    #> [[3]]$key$b
    #> [1] 3
    #> 
    #> 
    #> [[3]]$data
    #> shape: (1, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ b   ┆ 3.0 ┆ 2.0 │
    #> └─────┴─────┴─────┘
    #> 
    #> 
    #> [[4]]
    #> [[4]]$key
    #> [[4]]$key$a
    #> [1] "c"
    #> 
    #> [[4]]$key$b
    #> [1] 3
    #> 
    #> 
    #> [[4]]$data
    #> shape: (1, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ c   ┆ 3.0 ┆ 1.0 │
    #> └─────┴─────┴─────┘

``` r
# `as_nested_list = TRUE` should be used with `maintain_order = TRUE` or `include_key = TRUE`.
tryCatch(
  df$partition_by("a", "b", maintain_order = FALSE, include_key = FALSE, as_nested_list = TRUE),
  warning = function(w) w
)
```

    #> <simpleWarning in df$partition_by("a", "b", maintain_order = FALSE, include_key = FALSE,     as_nested_list = TRUE): cannot use `$partition_by` with `maintain_order = FALSE, include_key = FALSE, as_nested_list = TRUE`. Fall back to a flat list.>

``` r
# Example of using with lapply(), and printing the key and the data summary
df$partition_by("a", "b", maintain_order = FALSE, as_nested_list = TRUE) |>
  lapply(\(x) {
    sprintf("\nThe key value of `a` is %s and the key value of `b` is %s\n", x$key$a, x$key$b) |>
      cat()
    x$data$drop(names(x$key))$describe() |>
      print()
    invisible(NULL)
  }) |>
  invisible()
```

    #> 
    #> The key value of `a` is b and the key value of `b` is 2
    #> shape: (9, 2)
    #> ┌────────────┬──────┐
    #> │ statistic  ┆ c    │
    #> │ ---        ┆ ---  │
    #> │ str        ┆ f64  │
    #> ╞════════════╪══════╡
    #> │ count      ┆ 1.0  │
    #> │ null_count ┆ 0.0  │
    #> │ mean       ┆ 4.0  │
    #> │ std        ┆ null │
    #> │ min        ┆ 4.0  │
    #> │ 25%        ┆ 4.0  │
    #> │ 50%        ┆ 4.0  │
    #> │ 75%        ┆ 4.0  │
    #> │ max        ┆ 4.0  │
    #> └────────────┴──────┘
    #> 
    #> The key value of `a` is a and the key value of `b` is 1
    #> shape: (9, 2)
    #> ┌────────────┬──────────┐
    #> │ statistic  ┆ c        │
    #> │ ---        ┆ ---      │
    #> │ str        ┆ f64      │
    #> ╞════════════╪══════════╡
    #> │ count      ┆ 2.0      │
    #> │ null_count ┆ 0.0      │
    #> │ mean       ┆ 4.0      │
    #> │ std        ┆ 1.414214 │
    #> │ min        ┆ 3.0      │
    #> │ 25%        ┆ 3.0      │
    #> │ 50%        ┆ 5.0      │
    #> │ 75%        ┆ 5.0      │
    #> │ max        ┆ 5.0      │
    #> └────────────┴──────────┘
    #> 
    #> The key value of `a` is b and the key value of `b` is 3
    #> shape: (9, 2)
    #> ┌────────────┬──────┐
    #> │ statistic  ┆ c    │
    #> │ ---        ┆ ---  │
    #> │ str        ┆ f64  │
    #> ╞════════════╪══════╡
    #> │ count      ┆ 1.0  │
    #> │ null_count ┆ 0.0  │
    #> │ mean       ┆ 2.0  │
    #> │ std        ┆ null │
    #> │ min        ┆ 2.0  │
    #> │ 25%        ┆ 2.0  │
    #> │ 50%        ┆ 2.0  │
    #> │ 75%        ┆ 2.0  │
    #> │ max        ┆ 2.0  │
    #> └────────────┴──────┘
    #> 
    #> The key value of `a` is c and the key value of `b` is 3
    #> shape: (9, 2)
    #> ┌────────────┬──────┐
    #> │ statistic  ┆ c    │
    #> │ ---        ┆ ---  │
    #> │ str        ┆ f64  │
    #> ╞════════════╪══════╡
    #> │ count      ┆ 1.0  │
    #> │ null_count ┆ 0.0  │
    #> │ mean       ┆ 1.0  │
    #> │ std        ┆ null │
    #> │ min        ┆ 1.0  │
    #> │ 25%        ┆ 1.0  │
    #> │ 50%        ┆ 1.0  │
    #> │ 75%        ┆ 1.0  │
    #> │ max        ┆ 1.0  │
    #> └────────────┴──────┘
