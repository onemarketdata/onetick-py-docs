# otp.ops.get_top_level_query_name

### ``get_top_level_query_name()``

Returns the top level name of this query.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(QUERY_NAME=otp.ops.get_top_level_query_name())
>>> otp.run(data)
        Time                              QUERY_NAME
0 2003-12-01  industrious-alpaca.run.otq::main_query
```

##### SEE ALSO
**GET_TOP_LEVEL_QUERY_NAME** OneTick function

