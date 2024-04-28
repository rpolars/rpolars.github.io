

# Execute a SQL query against the LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L2134)

## Description

The calling frame is automatically registered as a table in the SQL
context under the name <code>“self”</code>. All DataFrames and
LazyFrames found in the <code>envir</code> are also registered, using
their variable name. More control over registration and execution
behaviour is available by the SQLContext object.

## Usage

<pre><code class='language-R'>LazyFrame_sql(query, ..., table_name = NULL, envir = parent.frame())
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="query">query</code>
</td>
<td>
A character of the SQL query to execute.
</td>
</tr>
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
<code id="table_name">table_name</code>
</td>
<td>
<code>NULL</code> (default) or a character of an explicit name for the
table that represents the calling frame (the alias <code>“self”</code>
will always be registered/available).
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

This functionality is considered <strong>unstable</strong>, although it
is close to being considered stable. It may be changed at any point
without it being considered a breaking change.

## Value

LazyFrame

## See Also

<ul>
<li>

SQLContext

</li>
</ul>

## Examples

``` r
library(polars)


lf1 = pl$LazyFrame(a = 1:3, b = 6:8, c = c("z", "y", "x"))
lf2 = pl$LazyFrame(a = 3:1, d = c(125, -654, 888))

# Query the LazyFrame using SQL:
lf1$sql("SELECT c, b FROM self WHERE a > 1")$collect()
```

    #> shape: (2, 2)
    #> ┌─────┬─────┐
    #> │ c   ┆ b   │
    #> │ --- ┆ --- │
    #> │ str ┆ i32 │
    #> ╞═════╪═════╡
    #> │ y   ┆ 7   │
    #> │ x   ┆ 8   │
    #> └─────┴─────┘

``` r
# Join two LazyFrames:
lf1$sql(
  "
SELECT self.*, d
FROM self
INNER JOIN lf2 USING (a)
WHERE a > 1 AND b < 8
"
)$collect()
```

    #> shape: (1, 4)
    #> ┌─────┬─────┬─────┬────────┐
    #> │ a   ┆ b   ┆ c   ┆ d      │
    #> │ --- ┆ --- ┆ --- ┆ ---    │
    #> │ i32 ┆ i32 ┆ str ┆ f64    │
    #> ╞═════╪═════╪═════╪════════╡
    #> │ 2   ┆ 7   ┆ y   ┆ -654.0 │
    #> └─────┴─────┴─────┴────────┘

``` r
# Apply SQL transforms (aliasing "self" to "frame") and subsequently
# filter natively (you can freely mix SQL and native operations):
lf1$sql(
  query = r"(
SELECT
 a,
MOD(a, 2) == 0 AS a_is_even,
(b::float / 2) AS 'b/2',
CONCAT_WS(':', c, c, c) AS c_c_c
FROM frame
ORDER BY a
)",
  table_name = "frame"
)$filter(!pl$col("c_c_c")$str$starts_with("x"))$collect()
```

    #> shape: (2, 4)
    #> ┌─────┬───────────┬─────┬───────┐
    #> │ a   ┆ a_is_even ┆ b/2 ┆ c_c_c │
    #> │ --- ┆ ---       ┆ --- ┆ ---   │
    #> │ i32 ┆ bool      ┆ f32 ┆ str   │
    #> ╞═════╪═══════════╪═════╪═══════╡
    #> │ 1   ┆ false     ┆ 3.0 ┆ z:z:z │
    #> │ 2   ┆ true      ┆ 3.5 ┆ y:y:y │
    #> └─────┴───────────┴─────┴───────┘
