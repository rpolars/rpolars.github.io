

# Execute SQL query against the registered data

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/sql.R#L68)

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

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #>  SELECT [col("mpg"), col("cyl"), col("disp"), col("hp"), col("drat"), col("wt"), col("qsec"), col("vs"), col("am"), col("gear"), col("carb")] FROM
    #>   FILTER [(col("cyl")) == (4)] FROM
    #> 
    #>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
