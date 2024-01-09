
# Split the string by a substring, restricted to returning at most <code>n</code> items

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__string.R#L728)

## Description

If the number of possible splits is less than <code>n-1</code>, the
remaining field elements will be null. If the number of possible splits
is <code>n-1</code> or greater, the last (nth) substring will contain
the remainder of the string.

## Usage

<pre><code class='language-R'>ExprStr_splitn(by, n)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_splitn_:_by">by</code>
</td>
<td>
Substring to split by.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_splitn_:_n">n</code>
</td>
<td>
Number of splits to make.
</td>
</tr>
</table>

## Value

Struct where each of <code>n</code> fields is of String type

## Examples

``` r
library(polars)

df = pl$DataFrame(s = c("a_1", NA, "c", "d_4"))
df$select(pl$col("s")$str$splitn(by = "_", 0))
```

    #> shape: (0, 1)
    #> ┌───────────┐
    #> │ s         │
    #> │ ---       │
    #> │ struct[1] │
    #> ╞═══════════╡
    #> └───────────┘

``` r
df$select(pl$col("s")$str$splitn(by = "_", 1))
```

    #> shape: (4, 1)
    #> ┌───────────┐
    #> │ s         │
    #> │ ---       │
    #> │ struct[1] │
    #> ╞═══════════╡
    #> │ {"a_1"}   │
    #> │ {null}    │
    #> │ {"c"}     │
    #> │ {"d_4"}   │
    #> └───────────┘

``` r
df$select(pl$col("s")$str$splitn(by = "_", 2))
```

    #> shape: (4, 1)
    #> ┌─────────────┐
    #> │ s           │
    #> │ ---         │
    #> │ struct[2]   │
    #> ╞═════════════╡
    #> │ {"a","1"}   │
    #> │ {null,null} │
    #> │ {"c",null}  │
    #> │ {"d","4"}   │
    #> └─────────────┘
