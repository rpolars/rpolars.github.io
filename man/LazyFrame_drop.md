

# Drop columns of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1022)

## Description

Drop columns of a LazyFrame

## Usage

<pre><code class='language-R'>LazyFrame_drop(columns)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_drop_:_columns">columns</code>
</td>
<td>
A character vector with the names of the column(s) to remove.
</td>
</tr>
</table>

## Value

LazyFrame

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$drop(c("mpg", "hp"))
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #>  SELECT [col("cyl"), col("disp"), col("drat"), col("wt"), col("qsec"), col("vs"), col("am"), col("gear"), col("carb")] FROM
    #>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
