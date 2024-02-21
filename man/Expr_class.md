

# Polars Expressions

## Description

Expressions are all the functions and methods that are applicable to a
Polars DataFrame or LazyFrame object. Some methods are under the
sub-namespaces.

## Sub-namespaces

<h4>
arr
</h4>

<code style="white-space: pre;">$arr</code> stores all array related
methods.

<h4>
bin
</h4>

<code style="white-space: pre;">$bin</code> stores all binary related
methods.

<h4>
cat
</h4>

<code style="white-space: pre;">$cat</code> stores all categorical
related methods.

<h4>
dt
</h4>

<code style="white-space: pre;">$dt</code> stores all temporal related
methods.

<h4>
list
</h4>

<code style="white-space: pre;">$list</code> stores all list related
methods.

<h4>
meta
</h4>

<code style="white-space: pre;">$meta</code> stores all methods for
working with the meta data.

<h4>
name
</h4>

<code style="white-space: pre;">$name</code> stores all name related
methods.

<h4>
str
</h4>

<code style="white-space: pre;">$str</code> stores all string related
methods.

<h4>
struct
</h4>

<code style="white-space: pre;">$struct</code> stores all struct related
methods.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = 1:2,
  b = list(1:2, 3:4),
  schema = list(a = pl$Int64, b = pl$Array(pl$Int64, 2))
)

df$select(pl$col("a")$first())
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i64 │
    #> ╞═════╡
    #> │ 1   │
    #> └─────┘

``` r
df$select(pl$col("b")$arr$sum())
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ b   │
    #> │ --- │
    #> │ i64 │
    #> ╞═════╡
    #> │ 3   │
    #> │ 7   │
    #> └─────┘
