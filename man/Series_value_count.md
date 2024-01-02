
# Value Counts as DataFrame

## Description

Value Counts as DataFrame

## Usage

<pre><code class='language-R'>Series_value_counts(sort = TRUE, parallel = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_value_count_:_sort">sort</code>
</td>
<td>
bool, default TRUE: sort table by value; FALSE: random
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_value_count_:_parallel">parallel</code>
</td>
<td>
bool, default FALSE, process multithreaded. Likely faster to have TRUE
for a big Series. If called within an already multithreaded context such
calling apply on a GroupBy with many groups, then likely slightly faster
to leave FALSE.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

pl$Series(iris$Species, "flower species")$value_counts()
```

    #> shape: (3, 2)
    #> ┌────────────────┬───────┐
    #> │ flower species ┆ count │
    #> │ ---            ┆ ---   │
    #> │ cat            ┆ u32   │
    #> ╞════════════════╪═══════╡
    #> │ setosa         ┆ 50    │
    #> │ versicolor     ┆ 50    │
    #> │ virginica      ┆ 50    │
    #> └────────────────┴───────┘
