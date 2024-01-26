

# Format an expression as a tree

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__meta.R#L169)

## Description

Format an expression as a tree

## Usage

<pre><code class='language-R'>ExprMeta_tree_format(return_as_string = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprMeta_tree_format_:_return_as_string">return_as_string</code>
</td>
<td>
Return the tree as a character vector? If <code>FALSE</code> (default),
the tree is printed in the console.
</td>
</tr>
</table>

## Value

If <code>return_as_string</code> is <code>TRUE</code>, a character
vector describing the tree.

If <code>return_as_string</code> is <code>FALSE</code>, prints the tree
in the console but doesn’t return any value.

## Examples

``` r
library(polars)

my_expr = (pl$col("foo") * pl$col("bar"))$sum()$over(pl$col("ham")) / 2
my_expr$meta$tree_format()
```

    #> 
    #>            0               1                2               3        
    #>    ┌─────────────────────────────────────────────────────────────────
    #>    │
    #>    │ ╭────────────╮ 
    #>  0 │ │ binary: // │ 
    #>    │ ╰────────────╯ 
    #>    │        │ ╰─────────────╮       
    #>    │        │               │       
    #>    │        │               │       
    #>    │  ╭──────────╮     ╭────────╮   
    #>  1 │  │ lit(2.0) │     │ window │   
    #>    │  ╰──────────╯     ╰────────╯   
    #>    │                        │ ╰─────────────╮        
    #>    │                        │               │        
    #>    │                        │               │        
    #>    │                  ╭──────────╮       ╭─────╮     
    #>  2 │                  │ col(ham) │       │ sum │     
    #>    │                  ╰──────────╯       ╰─────╯     
    #>    │                                        │        
    #>    │                                        │        
    #>    │                                        │        
    #>    │                                  ╭───────────╮  
    #>  3 │                                  │ binary: * │  
    #>    │                                  ╰───────────╯  
    #>    │                                        │ ╰──────────────╮       
    #>    │                                        │                │       
    #>    │                                        │                │       
    #>    │                                  ╭──────────╮     ╭──────────╮  
    #>  4 │                                  │ col(bar) │     │ col(foo) │  
    #>    │                                  ╰──────────╯     ╰──────────╯
