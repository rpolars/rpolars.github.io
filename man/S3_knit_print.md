
# knit print polars DataFrame

## Description

Mimics python-polars’ NotebookFormatter for HTML outputs.

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsDataFrame'
knit_print(x, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="knit_print.RPolarsDataFrame_:_x">x</code>
</td>
<td>
a polars DataFrame to knit_print
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="knit_print.RPolarsDataFrame_:_...">…</code>
</td>
<td>
additional arguments, not used
</td>
</tr>
</table>

## Details

Outputs HTML tables if the output format is HTML and the document’s
<code>df_print</code> option is not <code>“default”</code> or
<code>“tibble”</code>.

Or, the output format can be enforced with R’s <code>options</code>
function as follows:

<ul>
<li>

<code>options(polars.df_print = “default”)</code> for the default print
method.

</li>
<li>

<code>options(polars.df_print = “html”)</code> for the HTML table.

</li>
</ul>

## Value

invisible x or NULL
