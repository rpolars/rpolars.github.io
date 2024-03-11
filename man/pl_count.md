

# Return the number of non-null values in the column.

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/functions__lazy.R#L166)

## Description

This function is syntactic sugar for <code>pl$col(…)$count()</code>.

## Usage

<pre><code class='language-R'>pl_count(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_count_:_...">…</code>
</td>
<td>
Characters indicating the column names, passed to <code>pl$col()</code>.
See <code>?pl_col</code> for details.
</td>
</tr>
</table>

## Details

Calling this function without any arguments returns the number of rows
in the context. This way of using the function is deprecated. Please use
<code>pl$len()</code> instead.

## Value

Expression of data type UInt32

## See Also

<ul>
<li>

<code>pl$len()</code>

</li>
<li>

<code>\<Expr\>$count()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1, 2, NA),
  b = c(3, NA, NA),
  c = c("foo", "bar", "foo")
)

df$select(pl$count("a"))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 2   │
    #> └─────┘

``` r
df$select(pl$count(c("b", "c")))
```

    #> shape: (1, 2)
    #> ┌─────┬─────┐
    #> │ b   ┆ c   │
    #> │ --- ┆ --- │
    #> │ u32 ┆ u32 │
    #> ╞═════╪═════╡
    #> │ 1   ┆ 3   │
    #> └─────┴─────┘
