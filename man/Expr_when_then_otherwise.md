

# Make a when-then-otherwise expression

## Description

<code>when-then-otherwise</code> is similar to R <code>ifelse()</code>.
Always initiated by a
<code style="white-space: pre;">pl$when(\<condition\>)$then(\<value if
condition\>)</code>, and optionally followed by chaining one or more
<code style="white-space: pre;">$when(\<condition\>)$then(\<value if
condition\>)</code> statements.

## Usage

<pre><code class='language-R'>pl_when(...)

When_then(statement)

Then_when(...)

Then_otherwise(statement)

ChainedWhen_then(statement)

ChainedThen_when(...)

ChainedThen_otherwise(statement)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_when_then_otherwise_:_...">…</code>
</td>
<td>
Expr or something coercible to an Expr that returns a boolian each row.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_when_then_otherwise_:_statement">statement</code>
</td>
<td>
Expr or something coercible to an Expr value to insert in
<code style="white-space: pre;">$then()</code> or
<code style="white-space: pre;">$otherwise()</code>. A character vector
is parsed as column names.
</td>
</tr>
</table>

## Details

Chained when-then operations should be read like
<code style="white-space: pre;">if, else if, else if, …</code> in R, not
as <code style="white-space: pre;">if, if, if, …</code>, i.e. the first
condition that evaluates to <code>true</code> will be picked.

If none of the conditions are <code>true</code>, an optional
<code style="white-space: pre;">$otherwise(\<value if all statements are
false\>)</code> can be appended at the end. If not appended, and none of
the conditions are <code>true</code>, <code>null</code> will be
returned.

<code>RPolarsThen</code> objects and <code>RPolarsChainedThen</code>
objects (returned by <code style="white-space: pre;">$then()</code>)
stores the same methods as Expr.

## Value

<ul>
<li>

<code>pl$when()</code> returns a <code>When</code> object

</li>
<li>

<code style="white-space: pre;">\<When\>$then()</code> returns a
<code>Then</code> object

</li>
<li>

<code style="white-space: pre;">\<Then\>$when()</code> returns a
<code>ChainedWhen</code> object

</li>
<li>

<code style="white-space: pre;">\<ChainedWhen\>$then()</code> returns a
<code>ChainedThen</code> object

</li>
<li>

<code style="white-space: pre;">$otherwise()</code> returns an Expr
object.

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c(1, 3, 4), bar = c(3, 4, 0))

# Add a column with the value 1, where column "foo" > 2 and the value -1
# where it isn’t.
df$with_columns(
  val = pl$when(pl$col("foo") > 2)$then(1)$otherwise(-1)
)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬──────┐
    #> │ foo ┆ bar ┆ val  │
    #> │ --- ┆ --- ┆ ---  │
    #> │ f64 ┆ f64 ┆ f64  │
    #> ╞═════╪═════╪══════╡
    #> │ 1.0 ┆ 3.0 ┆ -1.0 │
    #> │ 3.0 ┆ 4.0 ┆ 1.0  │
    #> │ 4.0 ┆ 0.0 ┆ 1.0  │
    #> └─────┴─────┴──────┘

``` r
# With multiple when-then chained:
df$with_columns(
  val = pl$when(pl$col("foo") > 2)
  $then(1)
  $when(pl$col("bar") > 2)
  $then(4)
  $otherwise(-1)
)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ val │
    #> │ --- ┆ --- ┆ --- │
    #> │ f64 ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ 1.0 ┆ 3.0 ┆ 4.0 │
    #> │ 3.0 ┆ 4.0 ┆ 1.0 │
    #> │ 4.0 ┆ 0.0 ┆ 1.0 │
    #> └─────┴─────┴─────┘

``` r
# The `$otherwise` at the end is optional.
# If left out, any rows where none of the `$when()` expressions are evaluated to `true`,
# are set to `null`
df$with_columns(
  val = pl$when(pl$col("foo") > 2)$then(1)
)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬──────┐
    #> │ foo ┆ bar ┆ val  │
    #> │ --- ┆ --- ┆ ---  │
    #> │ f64 ┆ f64 ┆ f64  │
    #> ╞═════╪═════╪══════╡
    #> │ 1.0 ┆ 3.0 ┆ null │
    #> │ 3.0 ┆ 4.0 ┆ 1.0  │
    #> │ 4.0 ┆ 0.0 ┆ 1.0  │
    #> └─────┴─────┴──────┘

``` r
# Pass multiple predicates, each of which must be met:
df$with_columns(
  val = pl$when(
    pl$col("bar") > 0,
    pl$col("foo") %% 2 != 0
  )
  $then(99)
  $otherwise(-1)
)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬──────┐
    #> │ foo ┆ bar ┆ val  │
    #> │ --- ┆ --- ┆ ---  │
    #> │ f64 ┆ f64 ┆ f64  │
    #> ╞═════╪═════╪══════╡
    #> │ 1.0 ┆ 3.0 ┆ 99.0 │
    #> │ 3.0 ┆ 4.0 ┆ 99.0 │
    #> │ 4.0 ┆ 0.0 ┆ -1.0 │
    #> └─────┴─────┴──────┘

``` r
# In `$then()`, a character vector is parsed as column names
df$with_columns(baz = pl$when(pl$col("foo") %% 2 == 1)$then("bar"))
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬──────┐
    #> │ foo ┆ bar ┆ baz  │
    #> │ --- ┆ --- ┆ ---  │
    #> │ f64 ┆ f64 ┆ f64  │
    #> ╞═════╪═════╪══════╡
    #> │ 1.0 ┆ 3.0 ┆ 3.0  │
    #> │ 3.0 ┆ 4.0 ┆ 4.0  │
    #> │ 4.0 ┆ 0.0 ┆ null │
    #> └─────┴─────┴──────┘

``` r
# So use `pl$lit()` to insert a string
df$with_columns(baz = pl$when(pl$col("foo") %% 2 == 1)$then(pl$lit("bar")))
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬──────┐
    #> │ foo ┆ bar ┆ baz  │
    #> │ --- ┆ --- ┆ ---  │
    #> │ f64 ┆ f64 ┆ str  │
    #> ╞═════╪═════╪══════╡
    #> │ 1.0 ┆ 3.0 ┆ bar  │
    #> │ 3.0 ┆ 4.0 ┆ bar  │
    #> │ 4.0 ┆ 0.0 ┆ null │
    #> └─────┴─────┴──────┘
