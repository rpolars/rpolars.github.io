
# Tail of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/dataframe__frame.R#L786)

## Description

Get the last <code>n</code> rows.

## Usage

<pre><code class='language-R'>DataFrame_tail(n)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_tail_:_n">n</code>
</td>
<td>
Positive number not larger than 2^32.
</td>
</tr>
</table>

## Details

Any number will converted to u32. Negative raises error.

## Value

DataFrame
