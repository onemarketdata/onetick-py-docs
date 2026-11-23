# otp.ops.get_query_invocation_time

### ``get_query_invocation_time()``

Returns currently used context name.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(QUERY_INVOCATION_TIME=otp.ops.get_query_invocation_time())
>>> otp.run(data)
        Time       QUERY_INVOCATION_TIME
0 2003-12-01  2026-11-05 13:26:47.334088
```

##### SEE ALSO
**GET_QUERY_INVOCATION_TIME** OneTick function

