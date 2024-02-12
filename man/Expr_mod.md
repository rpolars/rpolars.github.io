

# Modulo two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L231)

## Description

The RHS can either be an Expr or an object that can be converted to a
literal (e.g an integer).

## Usage

<pre><code class='language-R'>Expr_mod(other)

# S3 method for class 'RPolarsExpr'
e1 %% e2
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_mod_:_other">other</code>
</td>
<td>
Literal or object that can be converted to a literal
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_mod_:_e1">e1</code>
</td>
<td>
Expr only
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_mod_:_e2">e2</code>
</td>
<td>
Expr or anything that can be converted to a literal
</td>
</tr>
</table>

## Details

Currently, the modulo operator behaves differently than in R, and not
guaranteed <code>x == (x %% y) + y \* (x %/% y)</code>.

## Value

Expr

## Examples

``` r
library(polars)

pl$select(pl$lit(-1:12) %% 3)$to_series()$to_vector()
```

    #>  [1] -1  0  1  2  0  1  2  0  1  2  0  1  2  0

``` r
# The example is **NOT** equivalent to the followings:
-1:12 %% 3
```

    #>  [1] 2 0 1 2 0 1 2 0 1 2 0 1 2 0

``` r
pl$select(-1:12 %% 3)$to_series()$to_vector()
```

    #>  [1] 2 0 1 2 0 1 2 0 1 2 0 1 2 0

``` r
# Not guaranteed `x == (x %% y) + y * (x %/% y)`
x = pl$lit(-1:12)
y = pl$lit(3)
pl$select(x == (x %% y) + y * (x %/% y))
```

    #> shape: (14, 1)
    #> ┌───────┐
    #> │       │
    #> │ ---   │
    #> │ bool  │
    #> ╞═══════╡
    #> │ false │
    #> │ true  │
    #> │ true  │
    #> │ true  │
    #> │ true  │
    #> │ …     │
    #> │ true  │
    #> │ true  │
    #> │ true  │
    #> │ true  │
    #> │ true  │
    #> └───────┘
