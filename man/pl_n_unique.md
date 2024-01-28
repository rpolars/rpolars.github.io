

# Count <code>n</code> unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/functions__lazy.R#L384)

## Description

Depending on the input type this function does different things:

## Usage

<pre><code class='language-R'>pl_n_unique(column)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_n_unique_:_column">column</code>
</td>
<td>

if dtype is:

<ul>
<li>

Series: call method n_unique() to return value of unique values.

</li>
<li>

String: syntactic sugar for <code>pl$col(column)$n_unique()</code>,
returns Expr

</li>
<li>

Expr: syntactic sugar for <code>column$n_unique()</code>, returns Expr

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr or value

## Examples

``` r
library(polars)

# column as Series
pl$n_unique(pl$Series(1:4)) == 4
```

    #> [1] TRUE

``` r
# column as String
expr = pl$n_unique("bob")
print(expr)
```

    #> polars Expr: col("bob").n_unique()

``` r
pl$DataFrame(bob = 1:4)$select(expr)
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ bob │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 4   │
    #> └─────┘

``` r
# colum as Expr
pl$DataFrame(bob = 1:4)$select(pl$n_unique(pl$col("bob")))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ bob │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 4   │
    #> └─────┘
