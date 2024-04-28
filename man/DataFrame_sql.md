

# Execute a SQL query against the DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L2480)

## Description

The calling frame is automatically registered as a table in the SQL
context under the name <code>“self”</code>. All DataFrames and
LazyFrames found in the <code>envir</code> are also registered, using
their variable name. More control over registration and execution
behaviour is available by the SQLContext object.

## Usage

<pre><code class='language-R'>DataFrame_sql(query, ..., table_name = NULL, envir = parent.frame())
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

DataFrame

## See Also

<ul>
<li>

SQLContext

</li>
</ul>

## Examples

``` r
library(polars)


df1 = pl$DataFrame(
  a = 1:3,
  b = c("zz", "yy", "xx"),
  c = as.Date(c("1999-12-31", "2010-10-10", "2077-08-08"))
)

# Query the DataFrame using SQL:
df1$sql("SELECT c, b FROM self WHERE a > 1")
```

    #> shape: (2, 2)
    #> ┌────────────┬─────┐
    #> │ c          ┆ b   │
    #> │ ---        ┆ --- │
    #> │ date       ┆ str │
    #> ╞════════════╪═════╡
    #> │ 2010-10-10 ┆ yy  │
    #> │ 2077-08-08 ┆ xx  │
    #> └────────────┴─────┘

``` r
# Join two DataFrames using SQL.
df2 = pl$DataFrame(a = 3:1, d = c(125, -654, 888))
df1$sql(
  "
SELECT self.*, d
FROM self
INNER JOIN df2 USING (a)
WHERE a > 1 AND EXTRACT(year FROM c) < 2050
"
)
```

    #> shape: (1, 4)
    #> ┌─────┬─────┬────────────┬────────┐
    #> │ a   ┆ b   ┆ c          ┆ d      │
    #> │ --- ┆ --- ┆ ---        ┆ ---    │
    #> │ i32 ┆ str ┆ date       ┆ f64    │
    #> ╞═════╪═════╪════════════╪════════╡
    #> │ 2   ┆ yy  ┆ 2010-10-10 ┆ -654.0 │
    #> └─────┴─────┴────────────┴────────┘

``` r
# Apply transformations to a DataFrame using SQL, aliasing "self" to "frame".
df1$sql(
  query = r"(
SELECT
a,
MOD(a, 2) == 0 AS a_is_even,
CONCAT_WS(':', b, b) AS b_b,
EXTRACT(year FROM c) AS year,
0::float AS 'zero'
FROM frame
)",
  table_name = "frame"
)
```

    #> shape: (3, 5)
    #> ┌─────┬───────────┬───────┬──────┬──────┐
    #> │ a   ┆ a_is_even ┆ b_b   ┆ year ┆ zero │
    #> │ --- ┆ ---       ┆ ---   ┆ ---  ┆ ---  │
    #> │ i32 ┆ bool      ┆ str   ┆ i32  ┆ f32  │
    #> ╞═════╪═══════════╪═══════╪══════╪══════╡
    #> │ 1   ┆ false     ┆ zz:zz ┆ 1999 ┆ 0.0  │
    #> │ 2   ┆ true      ┆ yy:yy ┆ 2010 ┆ 0.0  │
    #> │ 3   ┆ false     ┆ xx:xx ┆ 2077 ┆ 0.0  │
    #> └─────┴───────────┴───────┴──────┴──────┘
