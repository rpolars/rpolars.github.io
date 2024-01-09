
# concat another list

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__list.R#L127)

## Description

Concat the arrays in a Series dtype List in linear time.

## Usage

<pre><code class='language-R'>ExprList_concat(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_concat_:_other">other</code>
</td>
<td>
Rlist, Expr or column of same type as self.
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

df = pl$DataFrame(
  a = list("a", "x"),
  b = list(c("b", "c"), c("y", "z"))
)
df$select(pl$col("a")$list$concat(pl$col("b")))
```

    #> shape: (2, 1)
    #> ┌─────────────────┐
    #> │ a               │
    #> │ ---             │
    #> │ list[str]       │
    #> ╞═════════════════╡
    #> │ ["a", "b", "c"] │
    #> │ ["x", "y", "z"] │
    #> └─────────────────┘

``` r
df$select(pl$col("a")$list$concat(pl$lit("hello from R")))
```

    #> shape: (2, 1)
    #> ┌───────────────────────┐
    #> │ a                     │
    #> │ ---                   │
    #> │ list[str]             │
    #> ╞═══════════════════════╡
    #> │ ["a", "hello from R"] │
    #> │ ["x", "hello from R"] │
    #> └───────────────────────┘

``` r
df$select(pl$col("a")$list$concat(pl$lit(list("hello", c("hello", "world")))))
```

    #> shape: (2, 1)
    #> ┌─────────────────────────┐
    #> │ a                       │
    #> │ ---                     │
    #> │ list[str]               │
    #> ╞═════════════════════════╡
    #> │ ["a", "hello"]          │
    #> │ ["x", "hello", "world"] │
    #> └─────────────────────────┘
