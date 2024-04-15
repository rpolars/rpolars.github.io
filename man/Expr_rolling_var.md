

# Rolling variance

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__expr.R#L2438)

## Description

Compute the rolling (= moving) variance over the values in this array. A
window of length <code>window_size</code> will traverse the array. The
values that fill this window will (optionally) be multiplied with the
weights given by the <code>weight</code> vector.

## Usage

<pre><code class='language-R'>Expr_rolling_var(
  window_size,
  weights = NULL,
  min_periods = NULL,
  center = FALSE,
  by = NULL,
  closed = NULL,
  warn_if_unsorted = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rolling_var_:_window_size">window_size</code>
</td>
<td>

The length of the window. Can be a fixed integer size, or a dynamic
temporal size indicated by the following string language:

<ul>
<li>

1ns (1 nanosecond)

</li>
<li>

1us (1 microsecond)

</li>
<li>

1ms (1 millisecond)

</li>
<li>

1s (1 second)

</li>
<li>

1m (1 minute)

</li>
<li>

1h (1 hour)

</li>
<li>

1d (1 day)

</li>
<li>

1w (1 week)

</li>
<li>

1mo (1 calendar month)

</li>
<li>

1y (1 calendar year)

</li>
<li>

1i (1 index count) If the dynamic string language is used, the
<code>by</code> and <code>closed</code> arguments must also be set.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rolling_var_:_weights">weights</code>
</td>
<td>
An optional slice with the same length as the window that will be
multiplied elementwise with the values in the window.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rolling_var_:_min_periods">min_periods</code>
</td>
<td>
The number of values in the window that should be non-null before
computing a result. If <code>NULL</code>, it will be set equal to window
size.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rolling_var_:_center">center</code>
</td>
<td>
Set the labels at the center of the window
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rolling_var_:_by">by</code>
</td>
<td>
If the <code>window_size</code> is temporal for instance
<code>“5h”</code> or <code>“3s”</code>, you must set the column that
will be used to determine the windows. This column must be of DataType
Date or DateTime.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rolling_var_:_closed">closed</code>
</td>
<td>
Defines whether the temporal window interval is closed or not. Only
applicable if <code>by</code> is not <code>NULL</code> (in which case,
its possible values are <code>“left”</code>, <code>“right”</code>
(default), <code>“both”</code>, <code>“none”</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rolling_var_:_warn_if_unsorted">warn_if_unsorted</code>
</td>
<td>
Warn if data is not known to be sorted by <code>by</code> column (if
passed).
</td>
</tr>
</table>

## Details

If you want to compute multiple aggregation statistics over the same
dynamic window, consider using
<code style="white-space: pre;">$rolling()</code> this method can cache
the window size computation.

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(1, 3, 2, 4, 5, 6))$
  with_columns(roll_var = pl$col("a")$rolling_var(window_size = 2))
```

    #> shape: (6, 2)
    #> ┌─────┬──────────┐
    #> │ a   ┆ roll_var │
    #> │ --- ┆ ---      │
    #> │ f64 ┆ f64      │
    #> ╞═════╪══════════╡
    #> │ 1.0 ┆ null     │
    #> │ 3.0 ┆ 2.0      │
    #> │ 2.0 ┆ 0.5      │
    #> │ 4.0 ┆ 2.0      │
    #> │ 5.0 ┆ 0.5      │
    #> │ 6.0 ┆ 0.5      │
    #> └─────┴──────────┘
