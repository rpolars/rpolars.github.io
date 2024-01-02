
# List to Struct

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__list.R#L395)

## Description

List to Struct

## Usage

<pre><code class='language-R'>ExprList_to_struct(
  n_field_strategy = c("first_non_null", "max_width"),
  name_generator = NULL,
  upper_bound = 0
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_to_struct_:_n_field_strategy">n_field_strategy</code>
</td>
<td>
Strategy to determine the number of fields of the struct. default =
"first_non_null": set number of fields equal to the length of the first
non zero-length sublist. else ‘max_width’; else "max_width": set number
of fields as max length of all sublists.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_to_struct_:_name_generator">name_generator</code>
</td>
<td>
an R function that takes an R scalar double and outputs a string value.
It is a f64 because i32 might not be a big enough enumerate all. The
default (<code>NULL</code>) is equivalent to the R function
<code style="white-space: pre;">(idx) paste0(“field\_”, idx)</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_to_struct_:_upper_bound">upper_bound</code>
</td>
<td>
upper_bound A polars <code>LazyFrame</code> needs to know the schema at
all time. The caller therefore must provide an <code>upper_bound</code>
of struct fields that will be set. If set incorrectly, downstream
operation may fail. For instance an <code>all()$sum()</code> expression
will look in the current schema to determine which columns to select. It
is advised to set this value in a lazy query.
</td>
</tr>
</table>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(1:3, 1:2)))
df2 = df$select(pl$col("a")$list$to_struct(
  name_generator = \(idx) paste0("hello_you_", idx)
))
df2$unnest()
```

    #> shape: (2, 3)
    #> ┌─────────────┬─────────────┬─────────────┐
    #> │ hello_you_0 ┆ hello_you_1 ┆ hello_you_2 │
    #> │ ---         ┆ ---         ┆ ---         │
    #> │ i32         ┆ i32         ┆ i32         │
    #> ╞═════════════╪═════════════╪═════════════╡
    #> │ 1           ┆ 2           ┆ 3           │
    #> │ 1           ┆ 2           ┆ null        │
    #> └─────────────┴─────────────┴─────────────┘

``` r
df2$to_list()
```

    #> $a
    #> $a$hello_you_0
    #> [1] 1 1
    #> 
    #> $a$hello_you_1
    #> [1] 2 2
    #> 
    #> $a$hello_you_2
    #> [1]  3 NA
