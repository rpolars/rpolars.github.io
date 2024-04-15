

# Return the number of rows in the context.

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/functions__lazy.R#L160)

## Description

This is similar to <code style="white-space: pre;">COUNT(\*)</code> in
SQL.

## Usage

<pre><code class='language-R'>pl_len()
</code></pre>

## Value

Expression of data type UInt32

## See Also

<ul>
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

df$select(pl$len())
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ len │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 3   │
    #> └─────┘
