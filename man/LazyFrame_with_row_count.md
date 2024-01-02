
# Add a column for row indices

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/lazyframe__lazy.R#L265)

## Description

Add a new column at index 0 that counts the rows

## Usage

<pre><code class='language-R'>LazyFrame_with_row_count(name, offset = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_with_row_count_:_name">name</code>
</td>
<td>
string name of the created column
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_with_row_count_:_offset">offset</code>
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
df$with_row_count("idx")
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> WITH ROW COUNT
    #>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"

``` r
# but in R, we use a 1-index
df$with_row_count("idx", offset = 1)
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> WITH ROW COUNT
    #>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
