

# Concat polars objects

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/functions__eager.R#L56)

## Description

Concat polars objects

## Usage

<pre><code class='language-R'>pl_concat(
  ...,
  how = c("vertical", "vertical_relaxed", "horizontal", "diagonal", "diagonal_relaxed"),
  rechunk = TRUE,
  parallel = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_concat_:_...">…</code>
</td>
<td>
Either individual unpacked args or args wrapped in list(). Args can be
eager as DataFrame, Series and R vectors, or lazy as LazyFrame and Expr.
The first element determines the output of
<code style="white-space: pre;">$concat()</code>: if the first element
is lazy, a LazyFrame is returned; otherwise, a DataFrame is returned
(note that if the first element is eager, all other elements have to be
eager to avoid implicit collect).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_concat_:_how">how</code>
</td>
<td>
Bind direction. Can be "vertical" (like <code>rbind()</code>),
"horizontal" (like <code>cbind()</code>), or "diagonal". For
<code>“vertical”</code> and <code>“diagonal”</code>, adding the suffix
<code>“\_relaxed”</code> will cast columns to their shared supertypes.
For example, if we try to vertically concatenate two columns of types
<code>i32</code> and <code>f64</code>, using <code>how =
“vertical_relaxed”</code> will cast the column of type <code>i32</code>
to <code>f64</code> beforehand.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_concat_:_rechunk">rechunk</code>
</td>
<td>
Perform a rechunk at last.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_concat_:_parallel">parallel</code>
</td>
<td>
Only used for LazyFrames. If <code>TRUE</code> (default), lazy
computations may be executed in parallel.
</td>
</tr>
</table>

## Details

Categorical columns/Series must have been constructed while global
string cache enabled. See <code>pl$enable_string_cache()</code>.

## Value

DataFrame, Series, LazyFrame or Expr

## Examples

``` r
library(polars)

# vertical
l_ver = lapply(1:10, function(i) {
  l_internal = list(
    a = 1:5,
    b = letters[1:5]
  )
  pl$DataFrame(l_internal)
})
pl$concat(l_ver, how = "vertical")
```

    #> shape: (50, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ str │
    #> ╞═════╪═════╡
    #> │ 1   ┆ a   │
    #> │ 2   ┆ b   │
    #> │ 3   ┆ c   │
    #> │ 4   ┆ d   │
    #> │ 5   ┆ e   │
    #> │ …   ┆ …   │
    #> │ 1   ┆ a   │
    #> │ 2   ┆ b   │
    #> │ 3   ┆ c   │
    #> │ 4   ┆ d   │
    #> │ 5   ┆ e   │
    #> └─────┴─────┘

``` r
# horizontal
l_hor = lapply(1:10, function(i) {
  l_internal = list(
    1:5,
    letters[1:5]
  )
  names(l_internal) = paste0(c("a", "b"), i)
  pl$DataFrame(l_internal)
})
pl$concat(l_hor, how = "horizontal")
```

    #> shape: (5, 20)
    #> ┌─────┬─────┬─────┬─────┬───┬─────┬─────┬─────┬─────┐
    #> │ a1  ┆ b1  ┆ a2  ┆ b2  ┆ … ┆ a9  ┆ b9  ┆ a10 ┆ b10 │
    #> │ --- ┆ --- ┆ --- ┆ --- ┆   ┆ --- ┆ --- ┆ --- ┆ --- │
    #> │ i32 ┆ str ┆ i32 ┆ str ┆   ┆ i32 ┆ str ┆ i32 ┆ str │
    #> ╞═════╪═════╪═════╪═════╪═══╪═════╪═════╪═════╪═════╡
    #> │ 1   ┆ a   ┆ 1   ┆ a   ┆ … ┆ 1   ┆ a   ┆ 1   ┆ a   │
    #> │ 2   ┆ b   ┆ 2   ┆ b   ┆ … ┆ 2   ┆ b   ┆ 2   ┆ b   │
    #> │ 3   ┆ c   ┆ 3   ┆ c   ┆ … ┆ 3   ┆ c   ┆ 3   ┆ c   │
    #> │ 4   ┆ d   ┆ 4   ┆ d   ┆ … ┆ 4   ┆ d   ┆ 4   ┆ d   │
    #> │ 5   ┆ e   ┆ 5   ┆ e   ┆ … ┆ 5   ┆ e   ┆ 5   ┆ e   │
    #> └─────┴─────┴─────┴─────┴───┴─────┴─────┴─────┴─────┘

``` r
# diagonal
pl$concat(l_hor, how = "diagonal")
```

    #> shape: (50, 20)
    #> ┌──────┬──────┬──────┬──────┬───┬──────┬──────┬──────┬──────┐
    #> │ a1   ┆ b1   ┆ a2   ┆ b2   ┆ … ┆ a9   ┆ b9   ┆ a10  ┆ b10  │
    #> │ ---  ┆ ---  ┆ ---  ┆ ---  ┆   ┆ ---  ┆ ---  ┆ ---  ┆ ---  │
    #> │ i32  ┆ str  ┆ i32  ┆ str  ┆   ┆ i32  ┆ str  ┆ i32  ┆ str  │
    #> ╞══════╪══════╪══════╪══════╪═══╪══════╪══════╪══════╪══════╡
    #> │ 1    ┆ a    ┆ null ┆ null ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ 2    ┆ b    ┆ null ┆ null ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ 3    ┆ c    ┆ null ┆ null ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ 4    ┆ d    ┆ null ┆ null ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ 5    ┆ e    ┆ null ┆ null ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ …    ┆ …    ┆ …    ┆ …    ┆ … ┆ …    ┆ …    ┆ …    ┆ …    │
    #> │ null ┆ null ┆ null ┆ null ┆ … ┆ null ┆ null ┆ 1    ┆ a    │
    #> │ null ┆ null ┆ null ┆ null ┆ … ┆ null ┆ null ┆ 2    ┆ b    │
    #> │ null ┆ null ┆ null ┆ null ┆ … ┆ null ┆ null ┆ 3    ┆ c    │
    #> │ null ┆ null ┆ null ┆ null ┆ … ┆ null ┆ null ┆ 4    ┆ d    │
    #> │ null ┆ null ┆ null ┆ null ┆ … ┆ null ┆ null ┆ 5    ┆ e    │
    #> └──────┴──────┴──────┴──────┴───┴──────┴──────┴──────┴──────┘

``` r
# if two columns don't share the same type, concat() will error unless we use
# `how = "vertical_relaxed"`:
test = pl$DataFrame(x = 1L) # i32
test2 = pl$DataFrame(x = 1.0) # f64

pl$concat(test, test2, how = "vertical_relaxed")
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ x   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> │ 1.0 │
    #> └─────┘
