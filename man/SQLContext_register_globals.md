

# Register all polars DataFrames/LazyFrames found in the environment

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/sql.R#L193)

## Description

Automatically maps variable names to table names.

## Usage

<pre><code class='language-R'>SQLContext_register_globals(..., envir = parent.frame())
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="envir">envir</code>
</td>
<td>
The environment to search for polars DataFrames/LazyFrames.
</td>
</tr>
</table>

## Details

If a table with the same name is already registered, it will be
overwritten.

## Value

Returns the SQLContext object invisibly.

## See Also

<ul>
<li>

<code>\<SQLContext\>$register()</code>

</li>
<li>

<code>\<SQLContext\>$register_many()</code>

</li>
<li>

<code>\<SQLContext\>$unregister()</code>

</li>
</ul>

## Examples

``` r
library(polars)


df1 = pl$DataFrame(a = 1:3, b = c("x", NA, "z"))
df2 = pl$LazyFrame(a = 2:4, c = c("t", "w", "v"))

# Register frames directly from variables found in the current environment.
ctx = pl$SQLContext()$register_globals()
ctx$tables()
```

    #> [1] "df1" "df2"

``` r
ctx$execute(
  "SELECT a, b, c FROM df1 LEFT JOIN df2 USING (a) ORDER BY a DESC"
)$collect()
```

    #> shape: (3, 3)
    #> ┌─────┬──────┬──────┐
    #> │ a   ┆ b    ┆ c    │
    #> │ --- ┆ ---  ┆ ---  │
    #> │ i32 ┆ str  ┆ str  │
    #> ╞═════╪══════╪══════╡
    #> │ 3   ┆ z    ┆ w    │
    #> │ 2   ┆ null ┆ t    │
    #> │ 1   ┆ x    ┆ null │
    #> └─────┴──────┴──────┘
