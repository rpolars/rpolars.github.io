

# Create Categorical DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/datatype.R#L335)

## Description

Create Categorical DataType

## Usage

<pre><code class='language-R'>DataType_Categorical(ordering = "physical")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Categorical_:_ordering">ordering</code>
</td>
<td>
Either <code>“physical”</code> (default) or <code>“lexical”</code>.
</td>
</tr>
</table>

## Details

When a categorical variable is created, its string values (or "lexical"
values) are stored and encoded as integers ("physical" values) by order
of appearance. Therefore, sorting a categorical value can be done either
on the lexical or on the physical values. See Examples.

## Value

A Categorical DataType

## Examples

``` r
library(polars)

# default is to order by physical values
df = pl$DataFrame(x = c("z", "z", "k", "a", "z"), schema = list(x = pl$Categorical()))
df$sort("x")
```

    #> shape: (5, 1)
    #> ┌─────┐
    #> │ x   │
    #> │ --- │
    #> │ cat │
    #> ╞═════╡
    #> │ z   │
    #> │ z   │
    #> │ z   │
    #> │ k   │
    #> │ a   │
    #> └─────┘

``` r
# when setting ordering = "lexical", sorting will be based on the strings
df_lex = pl$DataFrame(
  x = c("z", "z", "k", "a", "z"),
  schema = list(x = pl$Categorical("lexical"))
)
df_lex$sort("x")
```

    #> shape: (5, 1)
    #> ┌─────┐
    #> │ x   │
    #> │ --- │
    #> │ cat │
    #> ╞═════╡
    #> │ a   │
    #> │ k   │
    #> │ z   │
    #> │ z   │
    #> │ z   │
    #> └─────┘
