# otp.ops.get_current_context_name

### ``get_current_context_name()``

Returns currently used context name.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(CONTEXT_NAME=otp.ops.get_current_context_name())
>>> otp.run(data)
        Time CONTEXT_NAME
0 2003-12-01      DEFAULT
```

##### SEE ALSO
**GET_CURRENT_CONTEXT_NAME** OneTick function

