

# show all public functions / objects

## Description

print any object(function, RPolarsDataType) available via
<code style="white-space: pre;">pl$</code>.

## Usage

<pre><code class='language-R'>pl_show_all_public_functions()
</code></pre>

## Examples

``` r
library(polars)

pl$show_all_public_functions()
```

    #> 
    #> 
    #>     polars public functions via pl$... ( pl_polars_env environment ):
    #>        [ all ; function ]
    #>        [ all_horizontal ; function ]
    #>        [ any_horizontal ; function ]
    #>        [ approx_n_unique ; function ]
    #>        [ Array ; function ]
    #>        [ Binary ; RPolarsDataType ]
    #>        [ Boolean ; RPolarsDataType ]
    #>        [ Categorical ; RPolarsDataType ]
    #>        [ class_names ; character ]
    #>        [ coalesce ; function ]
    #>        [ col ; function ]
    #>        [ concat ; function ]
    #>        [ concat_list ; function ]
    #>        [ concat_str ; function ]
    #>        [ corr ; function ]
    #>        [ count ; function ]
    #>        [ cov ; function ]
    #>        [ DataFrame ; function ]
    #>        [ Date ; RPolarsDataType ]
    #>        [ date_range ; function ]
    #>        [ Datetime ; function ]
    #>        [ disable_string_cache ; function ]
    #> 
    #>        dtypes ( list ):
    #>           [ Array ; function ]
    #>           [ Binary ; RPolarsDataType ]
    #>           [ Boolean ; RPolarsDataType ]
    #>           [ Categorical ; RPolarsDataType ]
    #>           [ Date ; RPolarsDataType ]
    #>           [ Datetime ; function ]
    #>           [ Float32 ; RPolarsDataType ]
    #>           [ Float64 ; RPolarsDataType ]
    #>           [ Int16 ; RPolarsDataType ]
    #>           [ Int32 ; RPolarsDataType ]
    #>           [ Int64 ; RPolarsDataType ]
    #>           [ Int8 ; RPolarsDataType ]
    #>           [ List ; function ]
    #>           [ Null ; RPolarsDataType ]
    #>           [ String ; RPolarsDataType ]
    #>           [ Struct ; function ]
    #>           [ Time ; RPolarsDataType ]
    #>           [ UInt16 ; RPolarsDataType ]
    #>           [ UInt32 ; RPolarsDataType ]
    #>           [ UInt64 ; RPolarsDataType ]
    #>           [ UInt8 ; RPolarsDataType ]
    #>           [ Unknown ; RPolarsDataType ]
    #>           [ Utf8 ; RPolarsDataType ]
    #> 
    #>        [ duration ; function ]
    #>        [ element ; function ]
    #>        [ enable_string_cache ; function ]
    #>        [ expr_to_r ; function ]
    #>        [ extra_auto_completion ; function ]
    #>        [ Field ; function ]
    #>        [ first ; function ]
    #>        [ Float32 ; RPolarsDataType ]
    #>        [ Float64 ; RPolarsDataType ]
    #>        [ fold ; function ]
    #>        [ from_epoch ; function ]
    #>        [ get_global_rpool_cap ; function ]
    #>        [ head ; function ]
    #>        [ implode ; function ]
    #>        [ Int16 ; RPolarsDataType ]
    #>        [ Int32 ; RPolarsDataType ]
    #>        [ Int64 ; RPolarsDataType ]
    #>        [ Int8 ; RPolarsDataType ]
    #>        [ is_schema ; function ]
    #>        [ last ; function ]
    #>        [ LazyFrame ; function ]
    #>        [ len ; function ]
    #>        [ List ; function ]
    #>        [ lit ; function ]
    #>        [ max ; function ]
    #>        [ max_horizontal ; function ]
    #>        [ mean ; function ]
    #>        [ median ; function ]
    #>        [ mem_address ; function ]
    #>        [ min ; function ]
    #>        [ min_horizontal ; function ]
    #>        [ n_unique ; function ]
    #>        [ Null ; RPolarsDataType ]
    #> 
    #>        numeric_dtypes ( list ):
    #>           [ Float32 ; RPolarsDataType ]
    #>           [ Float64 ; RPolarsDataType ]
    #>           [ Int16 ; RPolarsDataType ]
    #>           [ Int32 ; RPolarsDataType ]
    #>           [ Int64 ; RPolarsDataType ]
    #>           [ Int8 ; RPolarsDataType ]
    #> 
    #>        [ PTime ; function ]
    #>        [ raw_list ; function ]
    #>        [ read_csv ; function ]
    #>        [ read_ndjson ; function ]
    #>        [ read_parquet ; function ]
    #>        [ reduce ; function ]
    #>        [ rolling_corr ; function ]
    #>        [ rolling_cov ; function ]
    #>        [ same_outer_dt ; function ]
    #>        [ scan_csv ; function ]
    #>        [ scan_ipc ; function ]
    #>        [ scan_ndjson ; function ]
    #>        [ scan_parquet ; function ]
    #>        [ select ; function ]
    #>        [ Series ; function ]
    #>        [ set_global_rpool_cap ; function ]
    #>        [ show_all_public_functions ; function ]
    #>        [ show_all_public_methods ; function ]
    #>        [ SQLContext ; function ]
    #>        [ std ; function ]
    #>        [ String ; RPolarsDataType ]
    #>        [ struct ; function ]
    #>        [ Struct ; function ]
    #>        [ sum ; function ]
    #>        [ sum_horizontal ; function ]
    #>        [ tail ; function ]
    #>        [ thread_pool_size ; function ]
    #>        [ threadpool_size ; function ]
    #>        [ Time ; RPolarsDataType ]
    #>        [ UInt16 ; RPolarsDataType ]
    #>        [ UInt32 ; RPolarsDataType ]
    #>        [ UInt64 ; RPolarsDataType ]
    #>        [ UInt8 ; RPolarsDataType ]
    #>        [ Unknown ; RPolarsDataType ]
    #>        [ using_string_cache ; function ]
    #>        [ Utf8 ; RPolarsDataType ]
    #>        [ var ; function ]
    #>        [ when ; function ]
    #>        [ with_string_cache ; function ]
