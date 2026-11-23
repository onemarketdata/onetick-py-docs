# otp.ops.get_top_level_query_id

### ``get_top_level_query_id()``

Returns the unique ID of this query.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(QUERY_ID=otp.ops.get_top_level_query_id())
>>> otp.run(data)
        Time                                   QUERY_ID
0 2003-12-01  DESKTOP-EUI4SLI.7246.20261105180423.989.8
```

##### SEE ALSO
**GET_TOP_LEVEL_QUERY_ID** OneTick function

