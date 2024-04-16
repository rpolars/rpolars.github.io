

# Add a column for row indices

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/lazyframe__lazy.R#L353)

## Description

Add a new column at index 0 that counts the rows

## Usage

<pre><code class='language-R'>LazyFrame_with_row_index(name, offset = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_with_row_index_:_name">name</code>
</td>
<td>
string name of the created column
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_with_row_index_:_offset">offset</code>
</td>
<td>
positive integer offset for the start of the counter
</td>
</tr>
</table>

## Value

A new LazyFrame with a counter column in front

## Examples

``` r
library(polars)

df = pl$LazyFrame(mtcars)

# by default, the index starts at 0 (to mimic the behavior of Python Polars)
df$with_row_index("idx")
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> WITH ROW INDEX
    #>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"

``` r
# but in R, we use a 1-index
df$with_row_index("idx", offset = 1)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> WITH ROW INDEX
    #>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
