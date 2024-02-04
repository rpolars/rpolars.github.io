

# Execute SQL query against the registered data

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/sql.R#L76)

## Description

Parse the given SQL query and execute it against the registered frame
data.

## Usage

<pre><code class='language-R'>SQLContext_execute(query)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="SQLContext_execute_:_query">query</code>
</td>
<td>
A valid string SQL query.
</td>
</tr>
</table>

## Value

A LazyFrame

## Examples

``` r
library(polars)


query = "SELECT * FROM mtcars WHERE cyl = 4"

pl$SQLContext(mtcars = mtcars)$execute(query)
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #>  SELECT [col("mpg"), col("cyl"), col("disp"), col("hp"), col("drat"), col("wt"), col("qsec"), col("vs"), col("am"), col("gear"), col("carb")] FROM
    #>   FILTER [(col("cyl")) == (4)] FROM
    #> 
    #>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
