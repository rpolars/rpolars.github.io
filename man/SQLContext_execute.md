
# Execute SQL query against the registered data

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/sql.R#L78)

## Description

Parse the given SQL query and execute it against the registered frame
data.

## Usage

<pre><code class='language-R'>SQLContext_execute(query, eager = FALSE)
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
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="SQLContext_execute_:_eager">eager</code>
</td>
<td>
A logical flag indicating whether to collect the result immediately. If
FALSE (default), a LazyFrame is returned. If TRUE, a DataFrame is
returned.
</td>
</tr>
</table>

## Value

A LazyFrame or DataFrame depending on the value of <code>eager</code>.

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

``` r
pl$SQLContext(mtcars = mtcars)$execute(query, eager = TRUE)
```

    #> shape: (11, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 24.4 ┆ 4.0 ┆ 146.7 ┆ 62.0  ┆ … ┆ 1.0 ┆ 0.0 ┆ 4.0  ┆ 2.0  │
    #> │ 22.8 ┆ 4.0 ┆ 140.8 ┆ 95.0  ┆ … ┆ 1.0 ┆ 0.0 ┆ 4.0  ┆ 2.0  │
    #> │ 32.4 ┆ 4.0 ┆ 78.7  ┆ 66.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ 27.3 ┆ 4.0 ┆ 79.0  ┆ 66.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 26.0 ┆ 4.0 ┆ 120.3 ┆ 91.0  ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 2.0  │
    #> │ 30.4 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 2.0  │
    #> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
