

# Arithmetic operators for RPolars objects

## Description

Arithmetic operators for RPolars objects

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsExpr'
x + y

# S3 method for class 'RPolarsExpr'
x - y

# S3 method for class 'RPolarsExpr'
x * y

# S3 method for class 'RPolarsExpr'
x / y

# S3 method for class 'RPolarsExpr'
x ^ y

# S3 method for class 'RPolarsExpr'
x %% y

# S3 method for class 'RPolarsExpr'
x %/% y

# S3 method for class 'RPolarsSeries'
x + y

# S3 method for class 'RPolarsSeries'
x - y

# S3 method for class 'RPolarsSeries'
x * y

# S3 method for class 'RPolarsSeries'
x / y

# S3 method for class 'RPolarsSeries'
x ^ y

# S3 method for class 'RPolarsSeries'
x %% y

# S3 method for class 'RPolarsSeries'
x %/% y
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="S3_arithmetic_:_x">x</code>,
<code id="S3_arithmetic_:_y">y</code>
</td>
<td>
numeric type of RPolars objects or objects that can be coerced such.
Only <code>+</code> can take strings.
</td>
</tr>
</table>

## Value

A Polars object the same type as the input.

## See Also

<ul>
<li>

<code>\<Expr\>$add()</code>

</li>
<li>

<code>\<Expr\>$sub()</code>

</li>
<li>

<code>\<Expr\>$mul()</code>

</li>
<li>

<code>\<Expr\>$div()</code>

</li>
<li>

<code>\<Expr\>$pow()</code>

</li>
<li>

<code>\<Expr\>$mod()</code>

</li>
<li>

<code>\<Expr\>$floor_div()</code>

</li>
<li>

<code>\<Series\>$add()</code>

</li>
<li>

<code>\<Series\>$sub()</code>

</li>
<li>

<code>\<Series\>$mul()</code>

</li>
<li>

<code>\<Series\>$div()</code>

</li>
<li>

<code>\<Series\>$pow()</code>

</li>
<li>

<code>\<Series\>$mod()</code>

</li>
<li>

<code>\<Series\>$floor_div()</code>

</li>
</ul>

## Examples

``` r
library(polars)

pl$lit(5) + 10
```

    #> polars Expr: [(5.0) + (10.0)]

``` r
5 + pl$lit(10)
```

    #> polars Expr: [(5.0) + (10.0)]

``` r
pl$lit(5) + pl$lit(10)
```

    #> polars Expr: [(5.0) + (10.0)]

``` r
+pl$lit(1)
```

    #> polars Expr: 1.0

``` r
# This will not raise an error as it is not actually evaluated.
expr = pl$lit(5) + "10"
expr
```

    #> polars Expr: [(5.0) + (String(10))]

``` r
# Will raise an error as it is evaluated.
tryCatch(
  expr$to_series(),
  error = function(e) e
)
```

    #> <RPolarsErr_error: Execution halted with the following contexts
    #>    0: In R: in $select()
    #>    0: During function call [.main()]
    #>    1: Encountered the following error in Rust-Polars:
    #>          arithmetic on string and numeric not allowed, try an explicit cast first
    #> >

``` r
as_polars_series(5) + 10
```

    #> polars Series: shape: (1,)
    #> Series: '' [f64]
    #> [
    #>  15.0
    #> ]

``` r
+as_polars_series(5)
```

    #> polars Series: shape: (1,)
    #> Series: '' [f64]
    #> [
    #>  5.0
    #> ]

``` r
-as_polars_series(5)
```

    #> polars Series: shape: (1,)
    #> Series: '' [f64]
    #> [
    #>  -5.0
    #> ]
