

# Get polars environment variables

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/polars_envvars.R#L84)

## Description

Get polars environment variables

## Usage

<pre><code class='language-R'>polars_envvars()
</code></pre>

## Details

The following envvars are available (in alphabetical order, with the
default value in parenthesis):

<ul>
<li>

<code>POLARS_FMT_MAX_COLS</code> (<code>5</code>): Set the number of
columns that are visible when displaying tables. If negative, all
columns are displayed.

</li>
<li>

<code>POLARS_FMT_MAX_ROWS</code> (<code>8</code>): Set the number of
rows that are visible when displaying tables. If negative, all rows are
displayed. This applies to both <code>DataFrame</code> and
<code>Series</code>.

</li>
<li>

<code>POLARS_FMT_STR_LEN</code> (<code>32</code>): Maximum number of
characters to display;

</li>
<li>

<code>POLARS_FMT_TABLE_CELL_ALIGNMENT</code> (<code>“LEFT”</code>): set
the table cell alignment. Can be <code>“LEFT”</code>,
<code>“CENTER”</code>, <code>“RIGHT”</code>;

</li>
<li>

<code>POLARS_FMT_TABLE_CELL_LIST_LEN</code> (<code>3</code>): Maximum
number of elements of list variables to display;

</li>
<li>

<code>POLARS_FMT_TABLE_CELL_NUMERIC_ALIGNMENT</code>
(<code>“LEFT”</code>): Set the table cell alignment for numeric columns.
Can be <code>“LEFT”</code>, <code>“CENTER”</code>, <code>“RIGHT”</code>;

</li>
<li>

<code>POLARS_FMT_TABLE_DATAFRAME_SHAPE_BELOW</code> (<code>“0”</code>):
print the DataFrame shape information below the data when displaying
tables. Can be <code>“0”</code> or <code>“1”</code>.

</li>
<li>

<code>POLARS_FMT_TABLE_FORMATTING</code>
(<code>“UTF8_FULL_CONDENSED”</code>): Set table formatting style.
Possible values:

<ul>
<li>

<code>“ASCII_FULL”</code>: ASCII, with all borders and lines, including
row dividers.

</li>
<li>

<code>“ASCII_FULL_CONDENSED”</code>: Same as ASCII_FULL, but with dense
row spacing.

</li>
<li>

<code>“ASCII_NO_BORDERS”</code>: ASCII, no borders.

</li>
<li>

<code>“ASCII_BORDERS_ONLY”</code>: ASCII, borders only.

</li>
<li>

<code>“ASCII_BORDERS_ONLY_CONDENSED”</code>: ASCII, borders only, dense
row spacing.

</li>
<li>

<code>“ASCII_HORIZONTAL_ONLY”</code>: ASCII, horizontal lines only.

</li>
<li>

<code>“ASCII_MARKDOWN”</code>: ASCII, Markdown compatible.

</li>
<li>

<code>“UTF8_FULL”</code>: UTF8, with all borders and lines, including
row dividers.

</li>
<li>

<code>“UTF8_FULL_CONDENSED”</code>: Same as UTF8_FULL, but with dense
row spacing.

</li>
<li>

<code>“UTF8_NO_BORDERS”</code>: UTF8, no borders.

</li>
<li>

<code>“UTF8_BORDERS_ONLY”</code>: UTF8, borders only.

</li>
<li>

<code>“UTF8_HORIZONTAL_ONLY”</code>: UTF8, horizontal lines only.

</li>
<li>

<code>“NOTHING”</code>: No borders or other lines.

</li>
</ul>
</li>
<li>

<code>POLARS_FMT_TABLE_HIDE_COLUMN_DATA_TYPES</code> (<code>“0”</code>):
Hide table column data types (i64, f64, str etc.). Can be
<code>“0”</code> or <code>“1”</code>.

</li>
<li>

<code>POLARS_FMT_TABLE_HIDE_COLUMN_NAMES</code> (<code>“0”</code>): Hide
table column names. Can be <code>“0”</code> or <code>“1”</code>.

</li>
<li>

<code>POLARS_FMT_TABLE_HIDE_COLUMN_SEPARATOR</code> (<code>“0”</code>):
Hide the <code>“—”</code> separator between the column names and column
types. Can be <code>“0”</code> or <code>“1”</code>.

</li>
<li>

<code>POLARS_FMT_TABLE_HIDE_DATAFRAME_SHAPE_INFORMATION</code>
(<code>“0”</code>): Hide the DataFrame shape information when displaying
tables. Can be <code>“0”</code> or <code>“1”</code>.

</li>
<li>

<code>POLARS_FMT_TABLE_INLINE_COLUMN_DATA_TYPE</code>
(<code>“0”</code>): Moves the data type inline with the column name (to
the right, in parentheses). Can be <code>“0”</code> or <code>“1”</code>.

</li>
<li>

<code>POLARS_FMT_TABLE_ROUNDED_CORNERS</code> (<code>“0”</code>): Apply
rounded corners to UTF8-styled tables (only applies to UTF8 formats).

</li>
<li>

<code>POLARS_MAX_THREADS</code>
(<code style="white-space: pre;">\<variable\></code>): Maximum number of
threads used to initialize the thread pool. The thread pool is locked
once polars is loaded, so this envvar must be set before loading the
package.

</li>
<li>

<code>POLARS_STREAMING_CHUNK_SIZE</code>
(<code style="white-space: pre;">\<variable\></code>): Chunk size used
in the streaming engine. Integer larger than 1. By default, the chunk
size is determined by the schema and size of the thread pool. For some
datasets (esp. when you have large string elements) this can be too
optimistic and lead to Out of Memory errors.

</li>
<li>

<code>POLARS_TABLE_WIDTH</code>
(<code style="white-space: pre;">\<variable\></code>): Set the maximum
width of a table in characters.

</li>
<li>

<code>POLARS_VERBOSE</code> (<code>“0”</code>): Enable additional
verbose/debug logging.

</li>
<li>

<code>POLARS_WARN_UNSTABLE</code> (<code>“0”</code>): Issue a warning
when unstable functionality is used. Enabling this setting may help
avoid functionality that is still evolving, potentially reducing
maintenance burden from API changes and bugs. Can be <code>“0”</code> or
<code>“1”</code>.

</li>
</ul>

The following configuration options are present in the Python API but
currently cannot be changed in R: decimal separator, thousands
separator, float precision, float formatting, trimming decimal zeros.

## Value

<code>polars_envvars()</code> returns a named list where the names are
the names of environment variables and values are their values.

## Examples

``` r
library(polars)

polars_envvars()
```

    #> Environment variables:
    #> ========                                                                     
    #> POLARS_FMT_MAX_COLS                                                 5
    #> POLARS_FMT_MAX_ROWS                                                 8
    #> POLARS_FMT_STR_LEN                                                 32
    #> POLARS_FMT_TABLE_CELL_ALIGNMENT                                  LEFT
    #> POLARS_FMT_TABLE_CELL_LIST_LEN                                      3
    #> POLARS_FMT_TABLE_CELL_NUMERIC_ALIGNMENT                          LEFT
    #> POLARS_FMT_TABLE_DATAFRAME_SHAPE_BELOW                              0
    #> POLARS_FMT_TABLE_FORMATTING                       UTF8_FULL_CONDENSED
    #> POLARS_FMT_TABLE_HIDE_COLUMN_DATA_TYPES                             0
    #> POLARS_FMT_TABLE_HIDE_COLUMN_NAMES                                  0
    #> POLARS_FMT_TABLE_HIDE_COLUMN_SEPARATOR                              0
    #> POLARS_FMT_TABLE_HIDE_DATAFRAME_SHAPE_INFORMATION                   0
    #> POLARS_FMT_TABLE_INLINE_COLUMN_DATA_TYPE                            0
    #> POLARS_FMT_TABLE_ROUNDED_CORNERS                                    0
    #> POLARS_MAX_THREADS                                                  4
    #> POLARS_STREAMING_CHUNK_SIZE                                  variable
    #> POLARS_TABLE_WIDTH                                           variable
    #> POLARS_VERBOSE                                                      0
    #> POLARS_WARN_UNSTABLE                                                0
    #> 
    #> See `?polars::polars_envvars` for the definition of all envvars.

``` r
pl$DataFrame(x = "This is a very very very long sentence.")
```

    #> shape: (1, 1)
    #> ┌───────────────────────────────────┐
    #> │ x                                 │
    #> │ ---                               │
    #> │ str                               │
    #> ╞═══════════════════════════════════╡
    #> │ This is a very very very long se… │
    #> └───────────────────────────────────┘

``` r
Sys.setenv(POLARS_FMT_STR_LEN = 50)
pl$DataFrame(x = "This is a very very very long sentence.")
```

    #> shape: (1, 1)
    #> ┌─────────────────────────────────────────┐
    #> │ x                                       │
    #> │ ---                                     │
    #> │ str                                     │
    #> ╞═════════════════════════════════════════╡
    #> │ This is a very very very long sentence. │
    #> └─────────────────────────────────────────┘

``` r
# back to default
Sys.setenv(POLARS_FMT_STR_LEN = 32)
```
