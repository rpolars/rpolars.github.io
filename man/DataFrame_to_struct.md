

# Convert DataFrame to a Series of type "struct"

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/dataframe__frame.R#L966)

## Description

Convert DataFrame to a Series of type "struct"

## Usage

<pre><code class='language-R'>DataFrame_to_struct(name = "")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_to_struct_:_name">name</code>
</td>
<td>
Name given to the new Series
</td>
</tr>
</table>

## Value

A Series of type "struct"

## Examples

``` r
library(polars)

# round-trip conversion from DataFrame with two columns
df = pl$DataFrame(a = 1:5, b = c("one", "two", "three", "four", "five"))
s = df$to_struct()
s
```

    #> polars Series: shape: (5,)
    #> Series: '' [struct[2]]
    #> [
    #>  {1,"one"}
    #>  {2,"two"}
    #>  {3,"three"}
    #>  {4,"four"}
    #>  {5,"five"}
    #> ]

``` r
# convert to an R list
s$to_r()
```

    #> $a
    #> [1] 1 2 3 4 5
    #> 
    #> $b
    #> [1] "one"   "two"   "three" "four"  "five" 
    #> 
    #> attr(,"is_struct")
    #> [1] TRUE

``` r
# Convert back to a DataFrame
df_s = s$to_frame()
df_s
```

    #> shape: (5, 1)
    #> ┌─────────────┐
    #> │             │
    #> │ ---         │
    #> │ struct[2]   │
    #> ╞═════════════╡
    #> │ {1,"one"}   │
    #> │ {2,"two"}   │
    #> │ {3,"three"} │
    #> │ {4,"four"}  │
    #> │ {5,"five"}  │
    #> └─────────────┘
