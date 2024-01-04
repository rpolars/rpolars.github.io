
# Get list

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/expr__list.R#L149)

## Description

Get the value by index in the sublists.

## Usage

<pre><code class='language-R'>ExprList_get(index)

# S3 method for class 'RPolarsExprListNameSpace'
x[index]
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_get_:_index">index</code>
</td>
<td>
value to get
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_get_:_x">x</code>
</td>
<td>
RPolarsExprListNameSpace
</td>
</tr>
</table>

## Format

function

## Details

<code style="white-space: pre;">\[.RPolarsExprListNameSpace</code> used
as e.g. <code>pl$col(“a”)$arr\[0\]</code> same as
<code>pl$col(“a”)$get(0)</code>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(3:1, NULL, 1:2))) # NULL or integer() or list()
df$select(pl$col("a")$list$get(0))
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ a    │
    #> │ ---  │
    #> │ i32  │
    #> ╞══════╡
    #> │ 3    │
    #> │ null │
    #> │ 1    │
    #> └──────┘

``` r
df$select(pl$col("a")$list$get(c(2, 0, -1)))
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ a    │
    #> │ ---  │
    #> │ i32  │
    #> ╞══════╡
    #> │ 1    │
    #> │ null │
    #> │ 2    │
    #> └──────┘

``` r
df = pl$DataFrame(list(a = list(3:1, NULL, 1:2))) # NULL or integer() or list()
df$select(pl$col("a")$list[0])
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ a    │
    #> │ ---  │
    #> │ i32  │
    #> ╞══════╡
    #> │ 3    │
    #> │ null │
    #> │ 1    │
    #> └──────┘

``` r
df$select(pl$col("a")$list[c(2, 0, -1)])
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ a    │
    #> │ ---  │
    #> │ i32  │
    #> ╞══════╡
    #> │ 1    │
    #> │ null │
    #> │ 2    │
    #> └──────┘
