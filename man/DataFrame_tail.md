

# Tail of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/dataframe__frame.R#L813)

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
