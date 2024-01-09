
# pl$count

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/functions__lazy.R#L108)

## Description

Count the number of values in this column/context.

## Usage

<pre><code class='language-R'>pl_count(column = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_count_:_column">column</code>
</td>
<td>

if dtype is:

<ul>
<li>

Series: count length of Series

</li>
<li>

str: count values of this column

</li>
<li>

NULL: count the number of value in this context.

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr or value-count in case Series

## Examples

``` r
library(polars)


df = pl$DataFrame(
  a = c(1, 8, 3),
  b = c(4, 5, 2),
  c = c("foo", "bar", "foo")
)
df$select(pl$count())
```

    #> shape: (1, 1)
    #> ┌───────┐
    #> │ count │
    #> │ ---   │
    #> │ u32   │
    #> ╞═══════╡
    #> │ 3     │
    #> └───────┘

``` r
df$group_by("c", maintain_order = TRUE)$agg(pl$count())
```

    #> shape: (2, 2)
    #> ┌─────┬───────┐
    #> │ c   ┆ count │
    #> │ --- ┆ ---   │
    #> │ str ┆ u32   │
    #> ╞═════╪═══════╡
    #> │ foo ┆ 2     │
    #> │ bar ┆ 1     │
    #> └─────┴───────┘
