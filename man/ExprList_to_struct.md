

# Convert a Series of type <code>List</code> to <code>Struct</code>

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__list.R#L450)

## Description

Convert a Series of type <code>List</code> to <code>Struct</code>

## Usage

<pre><code class='language-R'>ExprList_to_struct(
  n_field_strategy = c("first_non_null", "max_width"),
  fields = NULL,
  upper_bound = 0
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n_field_strategy">n_field_strategy</code>
</td>
<td>
Strategy to determine the number of fields of the struct. If
<code>“first_non_null”</code> (default), set number of fields equal to
the length of the first non zero-length list. If
<code>“max_width”</code>, the number of fields is the maximum length of
a list.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="fields">fields</code>
</td>
<td>
If the name and number of the desired fields is known in advance, a list
of field names can be given, which will be assigned by index. Otherwise,
to dynamically assign field names, a custom R function that takes an R
double and outputs a string value can be used. If <code>NULL</code>
(default), fields will be <code>field_0</code>, <code>field_1</code> …
<code>field_n</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="upper_bound">upper_bound</code>
</td>
<td>
A <code>LazyFrame</code> needs to know the schema at all time. The
caller therefore must provide an <code>upper_bound</code> of struct
fields that will be set. If set incorrectly, downstream operation may
fail. For instance an <code>all()$sum()</code> expression will look in
the current schema to determine which columns to select. When operating
on a <code>DataFrame</code>, the schema does not need to be tracked or
pre-determined, as the result will be eagerly evaluated, so you can
leave this parameter unset.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(1:2, 1:3)))

# this discards the third value of the second list as the struct length is
# determined based on the length of the first non-empty list
df$with_columns(
  struct = pl$col("a")$list$to_struct()
)
```

    #> shape: (2, 2)
    #> ┌───────────┬───────────┐
    #> │ a         ┆ struct    │
    #> │ ---       ┆ ---       │
    #> │ list[i32] ┆ struct[2] │
    #> ╞═══════════╪═══════════╡
    #> │ [1, 2]    ┆ {1,2}     │
    #> │ [1, 2, 3] ┆ {1,2}     │
    #> └───────────┴───────────┘

``` r
# we can use "max_width" to keep all values
df$with_columns(
  struct = pl$col("a")$list$to_struct(n_field_strategy = "max_width")
)
```

    #> shape: (2, 2)
    #> ┌───────────┬────────────┐
    #> │ a         ┆ struct     │
    #> │ ---       ┆ ---        │
    #> │ list[i32] ┆ struct[3]  │
    #> ╞═══════════╪════════════╡
    #> │ [1, 2]    ┆ {1,2,null} │
    #> │ [1, 2, 3] ┆ {1,2,3}    │
    #> └───────────┴────────────┘

``` r
# pass a custom function that will name all fields by adding a prefix
df2 = df$with_columns(
  pl$col("a")$list$to_struct(
    fields = \(idx) paste0("col_", idx)
  )
)
df2
```

    #> shape: (2, 1)
    #> ┌───────────┐
    #> │ a         │
    #> │ ---       │
    #> │ struct[2] │
    #> ╞═══════════╡
    #> │ {1,2}     │
    #> │ {1,2}     │
    #> └───────────┘

``` r
df2$unnest()
```

    #> shape: (2, 2)
    #> ┌───────┬───────┐
    #> │ col_0 ┆ col_1 │
    #> │ ---   ┆ ---   │
    #> │ i32   ┆ i32   │
    #> ╞═══════╪═══════╡
    #> │ 1     ┆ 2     │
    #> │ 1     ┆ 2     │
    #> └───────┴───────┘

``` r
df2$to_list()
```

    #> $a
    #> $a$col_0
    #> [1] 1 1
    #> 
    #> $a$col_1
    #> [1] 2 2
