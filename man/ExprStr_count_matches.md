

# Count all successive non-overlapping regex matches

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__string.R#L653)

## Description

Count all successive non-overlapping regex matches

## Usage

<pre><code class='language-R'>ExprStr_count_matches(pattern, literal = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_count_matches_:_pattern">pattern</code>
</td>
<td>
A valid regex pattern
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_count_matches_:_literal">literal</code>
</td>
<td>
Treat pattern as a literal string.
</td>
</tr>
</table>

## Value

UInt32 array. Contains null if original value is null or regex capture
nothing.

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c("123 bla 45 asd", "xyz 678 910t"))
df$select(
  pl$col("foo")$str$count_matches(r"{(\d)}")$alias("count digits")
)
```

    #> shape: (2, 1)
    #> ┌──────────────┐
    #> │ count digits │
    #> │ ---          │
    #> │ u32          │
    #> ╞══════════════╡
    #> │ 5            │
    #> │ 6            │
    #> └──────────────┘

``` r
# we can use Polars expressions as pattern so that it's not necessarily the
# same for all rows
df2 = pl$DataFrame(foo = c("hello", "hi there"), pat = c("ell", "e"))
df2$with_columns(
  pl$col("foo")$str$count_matches(pl$col("pat"))$alias("reg_count")
)
```

    #> shape: (2, 3)
    #> ┌──────────┬─────┬───────────┐
    #> │ foo      ┆ pat ┆ reg_count │
    #> │ ---      ┆ --- ┆ ---       │
    #> │ str      ┆ str ┆ u32       │
    #> ╞══════════╪═════╪═══════════╡
    #> │ hello    ┆ ell ┆ 1         │
    #> │ hi there ┆ e   ┆ 2         │
    #> └──────────┴─────┴───────────┘
