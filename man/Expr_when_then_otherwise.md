
# when-then-otherwise Expr

## Description

Start a “when, then, otherwise” expression.

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
Into Expr into a boolean mask to branch by.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_when_then_otherwise_:_statement">statement</code>
</td>
<td>
Into Expr value to insert in when() or otherwise(). Strings interpreted
as column.
</td>
</tr>
</table>

## Details

when-then-otherwise is similar to R <code>ifelse()</code>.
<code>pl$when(condition)</code> takes a condition as input this will an
polars <code style="white-space: pre;">\<Expr\></code> which renderes to
a Boolean column. Then it is chained with a
<code style="white-space: pre;">$then(statement)</code> when arg
statement is an <code style="white-space: pre;">\<Expr\></code> which
produces a column with values if idealy all Boolean are true. Then
finally an <code style="white-space: pre;">$otherwise(statement)</code>
with values if false.
<code style="white-space: pre;">$otherwise()</code> returns an
<code>Expr</code> which will mix the
<code style="white-space: pre;">$then()</code> statement with the
<code style="white-space: pre;">$otherwise()</code> as given by the
when-condition.

State-machine details below. The state machine consists of 4 classes
<code style="white-space: pre;">\<When\></code>,
<code style="white-space: pre;">\<Then\></code>,
<code style="white-space: pre;">\<ChainedWhen\></code> &
<code style="white-space: pre;">\<ChainedThen\></code> and a starter
function <code>pl$when()</code> and the final expression class a polars
<code style="white-space: pre;">\<Expr\></code>.

<code>pl$when</code>return a
<code style="white-space: pre;">\<When\></code> object.
<code style="white-space: pre;">pl$when(condition) -\> \<When\></code>

<code style="white-space: pre;">\<When\></code> has a single public
method <code style="white-space: pre;">$then(statement)</code>
<code style="white-space: pre;">\<When\>$then(statement) -\>
\<Then\></code>

#the follow objects and methods are
<code style="white-space: pre;">\<Then\>$when(condition) -\>
\<ChainedWhen\></code>
<code style="white-space: pre;">\<Then\>$otherwise(statement) -\>
\<Expr\></code>
<code style="white-space: pre;">\<ChainedWhen\>$then(statement) -\>
\<ChainedThen\></code>
<code style="white-space: pre;">\<ChainedThen\>$when(condition) -\>
\<Expr\></code>
<code style="white-space: pre;">\<ChainedThen\>$otherwise(statement) -\>
\<Expr\></code>

This statemachine ensures only syntacticly allowed methods are availble
at any specific place in a nested when-then-otherwise expression.

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c(1, 3, 4), bar = c(3, 4, 0))

# Add a column with the value 1, where column "foo" > 2 and the value -1 where it isn’t.
df$with_columns(
  pl$when(pl$col("foo") > 2)$then(1)$otherwise(-1)$alias("val")
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
# With multiple when, thens chained:
df$with_columns(
  pl$when(pl$col("foo") > 2)
  $then(1)
  $when(pl$col("bar") > 2)
  $then(4)
  $otherwise(-1)
  $alias("val")
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
