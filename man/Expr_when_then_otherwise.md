

# Make a then-when-otherwise expression

## Description

<code>when-then-otherwise</code> is similar to R <code>ifelse()</code>.
This has to start with
<code style="white-space: pre;">pl$when(\<condition\>)$then(\<value if
condition\>)</code>. From there, it can:

<ul>
<li>

be chained to an <code style="white-space: pre;">$otherwise()</code>
statement that specifies the Expr to apply to the rows where the
condition is <code>FALSE</code>;

</li>
<li>

or be chained to other
<code style="white-space: pre;">$when()$then()</code> to specify more
cases, and then use <code style="white-space: pre;">$otherwise()</code>
when you arrive at the end of your chain. Note that one difference with
the Python implementation is that we <em>must</em> end the chain with an
<code style="white-space: pre;">$otherwise()</code> statement.

</li>
</ul>

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
Expr or something coercible to an Expr into a boolean mask to branch by.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_when_then_otherwise_:_statement">statement</code>
</td>
<td>
Expr or something coercible to an Expr value to insert in when() or
otherwise(). Strings interpreted as column.
</td>
</tr>
</table>

## Details

If you want to use the class of those <code>when-then-otherwise</code>
statement, note that there are 6 different classes corresponding to the
different steps:

<ul>
<li>

<code>pl$when()</code>returns a <code>When</code> object,

</li>
<li>

<code>pl$then()</code>returns a <code>Then</code> object,

</li>
<li>

<code style="white-space: pre;">\<Then\>$otherwise()</code>returns an
Expression object,

</li>
<li>

<code style="white-space: pre;">\<Then\>$when()</code>returns a
<code>ChainedWhen</code> object,

</li>
<li>

<code style="white-space: pre;">\<ChainedWhen\>$then()</code>returns a
<code>ChainedThen</code> object,

</li>
<li>

<code style="white-space: pre;">\<ChainedThen\>$otherwise()</code>returns
an Expression object.

</li>
</ul>

## Value

an polars object, see details.

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
