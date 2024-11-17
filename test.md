| OData URL Param | Method Params |
|-----|-----|
| filter | iv_filter_string |
| search | IO_TECH_REQUEST_CONTEXT->GET_SEARCH_STRING( ) |

---

To collect data sent during Create:-<br>
`IO_DATA_PROVIDER->READ_ENTRY_DATA( IMPORTING  ES_DATA  = <some_workarea> )`

---

During UPDATE_STREAM:- <br>
Following Parameters is used to get fileupload data from frontend
```
is_media_resource-mime_type.
is_media_resource-value.
```

During UPDATE_STREAM and GET_STREAM:- <br>
We use `copy_data_to_ref` to copy data from our workarea to output parameters.<br>

Note:- `copy_data_to_ref` is also used during `Execute_Action( ) i.e.. Function imports`

```
Data : wa         TYPE  zcl_z630am_odatawithba_mpc=>ts_file.
Data : wa_stream  TYPE  ty_s_media_resource.

...

wa_stream-mime_type = wa-filetype.
wa_stream-value  = wa-filecontent.

...

copy_data_to_ref( EXPORTING  is_data  = wa_Stream
                  CHANGING   cr_data   = er_Stream ).
```
---

**/iwbep/CL_MGW_DATA_UTIL** Standard Class can be used with below static methods
1. Filtering  ( select options)
2. Orderby ( Sorting  )
3. Paging   ( Paging  )	
---