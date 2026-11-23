# otp.ops.get_query_properties

### ``get_query_properties(show_values_set_via_dedicated_setters=False)``

Returns query properties as a comma separated list of name-value pairs.

* **Parameters:**
  **show_values_set_via_dedicated_setters** (*bool*) – 

  If set to True, the query properties that have dedicated setters,
  i.e. *APPLY_TIMES_DAILY*, *BATCH_SIZE*, *MAX_CONCURRENCY*, and *PROCESS_DBS_CONCURRENTLY*,
  and the values of which are not equal to the default values for those properties,
  will be included into the result of this function.

  Default is False.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(QUERY_PROPERTIES=otp.ops.get_query_properties())
>>> otp.run(data, query_properties={'ALLOW_GRAPH_REUSE': 'TRUE'})
        Time                            QUERY_PROPERTIES
0 2003-12-01  ALLOW_GRAPH_REUSE='TRUE',USE_FT='FALSE'...
```

##### SEE ALSO
**GET_QUERY_PROPERTIES** OneTick function

